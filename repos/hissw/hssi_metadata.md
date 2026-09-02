# HSSI Metadata Extraction Results

**HSSI Software ID:** 0321f375-4f6c-47d8-9181-125b0274ee6b
**Repository:** https://github.com/wtbarnes/hissw
**Source Revision:** 39765a546300ab2e56598bf45d57fc4b5dd735db
**Extraction Date:** 2026-09-01
**Validation Date:** 2026-09-02
**Validation Status:** PASS

---

## Scope note — read this before the field notes

`hissw` is a **language bridge**, not a science package. Its Python modules render Jinja2 templates
into IDL/SSW source, write them to a temporary directory, execute them in an `sswidl` or `idl` shell
via `subprocess`, and load the resulting IDL save file back with `scipy.io.readsav`. All of the
solar physics lives in the *user's* IDL script and in the SolarSoft tree, never in hissw.

That distinction governs several fields below, and it is applied consistently in both directions:
**hissw is credited for what hissw's own code does, and not for what SolarSoft does on its behalf.**
The same rule that keeps `Solar Environment` in Field 5 (the form asks what a package is *commonly
used or intended for*, and there is exactly one vocabulary value meaning "solar, unspecified") is
the rule that leaves Field 22 empty (every Phenomena value is a *specific* phenomenon, and hissw
implements none of them) and that keeps `Data Access and Retrieval` out of Field 4 (SolarSoft
retrieves data; hissw does not).

A second scope point: at the pinned revision the repository has no `CITATION.cff`, no
`codemeta.json`, no `AUTHORS`/`CONTRIBUTORS` file, no `.zenodo.json`, and no `CHANGELOG`. The
authoritative non-repository sources are therefore the two Zenodo lineages, PyPI, the PyHC community
registry, ORCID, and journal bylines.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder is the catalogue convention for a dossier that is not itself a submission; the
submitter identity is supplied at submission time and is not a property of the software.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.5519495

Carried over from the existing HSSI record and confirmed against Zenodo: this is the **concept DOI**
of the lineage that is still receiving releases, and `https://zenodo.org/api/records/7352323`
reports `conceptdoi: 10.5281/zenodo.5519495` for the current v2.3 record.

**There are two Zenodo concept lineages for hissw, and only one is correct here.** The retired
lineage is `10.5281/zenodo.4039909`, holding records `4039910` (v1.0, 2018-09-12) and `4039915`
(v1.1, 2019-07-26), both titled simply `hissw`. The live lineage is `10.5281/zenodo.5519495`,
holding `5519496` (v1.2), `6640421` (v2.0), `6678107` (v2.1), `7017205` (v2.2) and `7352323` (v2.3),
all titled `wtbarnes/hissw: vX`. Every record in both lineages carries an `isSupplementTo` relation
to `https://github.com/wtbarnes/hissw/tree/<tag>`, the signature of the GitHub–Zenodo integration
rather than a manual deposit — which is why Field 11 records Zenodo as publisher.

**Durable warning about DOI autofill on this record.** The live lineage's records declare `license:
{"id": "other-open"}`, which is **wrong** — the repository has shipped an MIT `LICENSE` since 2017
and both setup.cfg and PyPI carry the `License :: OSI Approved :: MIT License` classifier. The
retired lineage records the licence correctly as `mit-license`. Anything derived by DOI autofill
from `10.5281/zenodo.5519495` must have its licence (and its dates) re-derived from the repository;
see Field 15.

**README badge anomaly, recorded so a future agent does not "fix" the wrong half.** In `README.md`
at the pinned revision the DOI badge *image* is
`https://zenodo.org/badge/DOI/10.5281/zenodo.4039915.svg` — the retired lineage's v1.1 record —
while the badge *link* target is `https://doi.org/10.5281/zenodo.5519495`, the current concept DOI.
The link is right and the image is stale. HSSI stores the link target, which is the correct value;
the badge image is an upstream cosmetic defect in the README, not a metadata error to import.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/wtbarnes/hissw

Carried over from the existing HSSI record and reconfirmed live: the GitHub API reports `full_name:
wtbarnes/hissw`, `archived: false`, `disabled: false`, `default_branch: main`. Redirect probes for
plausible predecessor names (`scivision/hissw`, `rice-solar-physics/hissw`, `wtbarnes/hiss`) all
return 404 with no redirect, so this repository has not been renamed or transferred and no older URL
needs preserving.

### 4. Software Functionality (RECOMMENDED — treated as critical)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: File Format Conversion
- Servers and Environments
- Servers and Environments: Software or Environment Container

**`Servers and Environments` is recorded** because the taxonomy requires a subcategory's parent to
be selected alongside it, and before this refresh the record carried `Servers and Environments:
Software or Environment Container` with no parent. Independently of that rule, the bare parent is
the most honest one-line answer to "what kind of software is this": hissw's public API centres on a
single class named `Environment`, whose docstring reads "Environment for running SSW and IDL
scripts" and whose job is to assemble and run a configured IDL/SSW runtime. That class is not quite
the entire public surface — `hissw/util.py` also defines the exceptions `SSWIDLError` and
`IDLLicenseError`, which `Environment.run` raises at its callers and which are therefore part of the
contract a user codes against — but the package's central abstraction is literally an *Environment*.

**`Servers and Environments: Software or Environment Container` is kept**, with the ambiguity
recorded honestly rather than resolved away. hissw is not a container in the Docker/Singularity
sense, and a searcher specifically hunting for images may not have hissw in mind. But hissw does
construct a self-contained execution environment — `shell_script()` templates a tcsh startup that
sets `SSW`, `SSW_INSTR` and `IDL_DIR` and sources `$SSW/gen/setup/setup.ssw`; `command_script()`
builds the IDL path; the whole thing runs inside a `tempfile.TemporaryDirectory()` that is torn down
afterwards. Weighed against that, the five subcategories under this parent are data serving,
distribution/access, high performance computing, infrastructure as code, and this one; none of the
other four describes assembling and running a configured runtime, which is precisely what hissw
does. The value was kept deliberately, on the balance of those two considerations rather than on a
clean fit.

**`Data Processing and Analysis: File Format Conversion` is kept**, and it is the concrete data
capability hissw actually implements. The conversion is bidirectional and both halves are hissw's
own code: on the way in, `hissw/filters.py` turns Python objects into IDL literal syntax
(`string_list_filter` quotes a list of strings for IDL; `force_double_precision_filter` renders a
float as an integer-ratio division so IDL receives full precision; `units_filter` reduces an
`astropy.units.Quantity` to a bare number); on the way out, `Environment.run` calls
`readsav(save_filename)` to turn an IDL save file into Python arrays. `Data Processing and Analysis`
is its required parent.

**`Data Processing and Analysis: Data Access and Retrieval` is not recorded.** HSSI carried this
value before this refresh, and the evidence does not support it. hissw contains no network client,
no archive query and no download path: there is no HTTP or FTP call anywhere in `hissw/`, and Field
17 (Data Sources) is correspondingly empty. The earlier justification was that hissw gives access
to IDL/SSW functionality from Python, which conflates *function* access with *data* access. The
user-facing consequence is the deciding one: this category is where archive clients and query
interfaces live — the tools someone reaches for when they need to *fetch* data — and hissw fetches
nothing. SolarSoft legitimately carries this category because SSW does contain retrieval routines;
hissw's claim on it was inherited from SolarSoft, and it cost a searcher a false hit in a large,
heavily-used filter.

**New values considered and rejected.** The vocabulary was reviewed for an execution-, workflow-, or
scripting-oriented category that the earlier extraction could not have chosen, since that is the
axis along which hissw is hardest to classify. There is none. The two nearest candidates were
rejected: `Mission-related: Orchestration`, because its parent scopes it to mission ground-system
software and hissw serves no mission; and `Servers and Environments: Infrastructure as Code`,
because that category is about provisioning and deploying computing infrastructure declaratively,
and hissw's templated `startup.sh` configures one short-lived local shell rather than any
infrastructure. `Data Processing and Analysis: Processing` and `: Analysis` were also rejected:
hissw performs no scientific processing or analysis of its own, and its only transformations are the
serialization steps already captured by `File Format Conversion`. Admitting a catch-all here would
contradict the same rule that keeps `Data Access and Retrieval` out, two paragraphs up.

### 5. Related Region (RECOMMENDED — treated as critical)
**Value:** Solar Environment

Carried over from the existing HSSI record, and re-derived rather than inherited, because there is a
real argument on both sides.

**The argument against any Region:** no module under `hissw/` implements solar physics. The only
solar references in the package are a docstring example of the `ssw_packages` argument (`'sdo/aia'`,
`'chianti'`) and the AIA smoke test; no module and none of the three templates contains a physical
constant, an instrument response, or a coordinate system. `Environment(idl_only=True)` runs plain
IDL with no SolarSoft at all.

**Why `Solar Environment` is nonetheless the right answer.** The form's own instruction for this
field is "Select all physical regions the software's functionality is commonly used or intended
for." — a use-and-intent standard, not a code-content standard. On that standard hissw is
unambiguously solar, and the decisive point is *what it wraps*. hissw is a bridge with no domain
code of its own, structurally like any other language wrapper — but the library it exists to run is
itself the solar physics IDL library. `README.md` states the requirement outright: "Additionally,
you'll need a local install of IDL and the [Solarsoft library](http://www.lmsal.com/solarsoft/)."
The package is named for SSW; the author's own `setup.cfg` keywords are `solar`, `sun`, `ssw`,
`solar-physics`, `idl`, `sswidl`, `solarsoft`; the repository's GitHub topics include
`solar-physics`; it is listed in the PyHC community registry; and both refereed papers that cite
hissw (Field 27) are solar physics papers. The solar character is therefore a property of hissw's
purpose, not merely of the community that happens to use it — which is what distinguishes it from a
generic wrapper that a solar physicist might also happen to run.

Decided from the searcher's side: someone browsing HSSI's `Solar Environment` listing for solar
tooling would recognise hissw as the Python-to-SolarSoft bridge and be glad to find it there, and
nobody scanning that listing is annoyed by its presence. That is the test this field turns on.

**Why no finer solar region.** The Region vocabulary is flat: `Solar Environment` does not imply
`Corona`, and choosing `Corona`, `Chromosphere`, `Photosphere`, `Solar Interior` or `Solar Wind`
would assert a specificity hissw does not have. `Solar Environment` is the one value that says
exactly what the evidence supports — solar domain, no particular region — so it is selected and
every finer value is rejected. All non-solar regions are rejected for the obvious reason.

This is the point at which Field 5 and Field 22 diverge, and the divergence is deliberate: Field 5
has a vocabulary value meaning "solar, unspecified" and Field 22 does not. See Field 22.

### 6. Authors (MANDATORY)

**Author 1**
- **Author Name:** Will Barnes
- **Author Identifier:** https://orcid.org/0000-0001-9642-6089
- **Affiliations:**
  - American University — https://ror.org/052w4zt36
  - Department of Physics, American University — no ROR (department-level; ROR does not mint
    identifiers for sub-institutional units)
  - Goddard Space Flight Center — https://ror.org/0171mag52
  - United States Naval Research Laboratory — https://ror.org/04d23a975

**Author 2**
- **Author Name:** Bin Chen
- **Author Identifier:** https://orcid.org/0000-0002-0660-3350
- **Affiliation:** New Jersey Institute of Technology — https://ror.org/05e74xb87

Both authors are carried over from the existing HSSI record and are corroborated by the Zenodo
records for v1.2 through v2.3, which credit `Will Barnes` and `Bin Chen`. `setup.cfg` names only
`author = Will Barnes` / `author_email = will.t.barnes@gmail.com`; there is no `CITATION.cff` or
`codemeta.json` at the pinned revision to consult. Neither author is dropped.

**Bin Chen's inclusion is correct even though his repository footprint is small.** His only commit
on the pinned lineage is `0c218d9a2b5e74f1ab8cd094fc46e7cd6131205c` (2021-01-07), a two-line typo
fix in `docs/examples/aia_example.md`. His authorship credit comes from the author's own choice:
Will Barnes listed him as a creator on every Zenodo record of the live lineage, and both published
papers that cite hissw cite it as "Barnes, W., & Chen, B." A future agent should not read the thin
commit history as grounds for removing him.

**Bin Chen's ORCID — identity evidence.** "Bin Chen" is a common name, so the match was made on
converging evidence rather than the name: the ORCID record `0000-0002-0660-3350` gives employment
"New Jersey Institute of Technology, Department of Physics, Associate Professor" from 2019, a PhD
from the University of Virginia, and a works list dominated by solar radio astronomy (CME magnetic
fields, microwave imaging spectroscopy, OVRO-LWA). That matches the `bin.chen@njit.edu` commit
address and the `New Jersey Institute of Technology` affiliation on the Zenodo records exactly.

**Durable platform caution — an ORCID must never be introduced through a routine metadata update.**
Supplying an ORCID for an author whose stored record carries no identifier does not fill that record
in: it resolves to a *different* person, creating a second record and orphaning the original along
with its affiliation. That is general platform behaviour, and it is why Bin Chen's ORCID could not be
supplied the ordinary way — his catalogued author record held no identifier before this refresh. It
was applied instead by a direct database correction on 2026-09-02, which kept his New Jersey
Institute of Technology affiliation attached and created no duplicate record for him. The identifier
above is therefore an applied value rather than a target state, and the caution stands for any author
found in the same position later.

**Will Barnes's four affiliations were examined individually and all four are kept.** His ORCID
record is stale (its most recent employment is the 2020 National Research Council associateship
hosted at NRL, with no end date and no later entries), so journal bylines were used as the primary
evidence:

- *Department of Physics, American University* and *Goddard Space Flight Center* — **current.**
  Every refereed byline from 2023 onward carries both, in one order or the other. The complete
  affiliation field of 2025ApJ...994..139J, for example, is "Department of Physics, American
  University, Washington, DC 20016, USA; Heliophysics Science Division, NASA Goddard Space Flight
  Center, Greenbelt, MD 20771, USA". The institution-level American University entry and the
  department-level entry are both retained: the department entry matches the departmental form most
  of those bylines use — a few give plain "American University" with a street address instead — and
  the institution entry carries the ROR.
- *United States Naval Research Laboratory* — **real but past**, and deliberately kept. His bylines
  from 2020 through mid-2022 place him at NRL through a National Research Council associateship.
  These affiliation fields are multi-part, and they are quoted here in full rather than trimmed to
  their NRL segment, because the omitted segments bear on the Rice question below.
  2021ApJ...919..132B reads "National Research Council Postdoctoral Research Associate residing at
  the Naval Research Laboratory, Washington, DC 20375, USA; Department of Physics & Astronomy, Rice
  University, Houston, TX 77005-1827, USA", and 2022ApJ...933..106R words the same arrangement as
  "National Research Council Research Associate Residing at the Naval Research Laboratory,
  Washington, DC 20375, USA; NASA Goddard Space Flight Center, Heliophysics Sciences Division,
  Greenbelt, MD 20771, USA; Department of Physics, American University, Washington, DC 20016, USA".
  NRL then disappears: no refereed byline from 2023 onward names it. That window covers the releases
  of hissw v1.2 through v2.3, so NRL was one of his affiliations throughout the period in which the
  currently-catalogued version was produced — the 2022 byline shows American University and Goddard
  already standing alongside it by then, so keeping all three is the accurate picture rather than a
  choice among them. NRL is also recorded on a **shared** Person record used by every HSSI entry
  Will Barnes authors, several of which date from that period. Removing it would rewrite those
  entries' authorship context to fix nothing. It stays.

**Rice University was considered and is deliberately not recorded.** It has the strongest
historical claim of any candidate, and the whole of that claim is set out here so a future agent
does not rediscover it piecemeal and reopen the question. hissw was created at Rice: the first
commits are authored from `wtb2@rice.edu`, the `LICENSE` reads "Copyright (c) 2017 Will Barnes", and
both records of the retired Zenodo lineage give "Barnes, Will", affiliation "Rice University", with
his ORCID attached — those two are the only records in either lineage that carry an ORCID at all.
The association also outlasts his time in residence: the 2021 byline quoted above still names
"Department of Physics & Astronomy, Rice University" as the second half of his affiliation field,
most plausibly a retained or courtesy appointment.

It is nonetheless not recorded, and the reason is the user-facing one, not a claim about when the
association ended. Rice is a years-stale affiliation. Will Barnes is stored on a single Person record
shared by every HSSI entry he authors, so adding a fifth organisation would lengthen his author
display on all of those pages while telling a reader nothing about where the work is done now — cost
to every reader, benefit to none.

An earlier version of this note rested the rejection on his having left Rice in 2019. That premise
is unsound — the 2021 byline is inconsistent with a clean 2019 departure — and it is recorded here
as superseded precisely so it is not picked up and reused as though it were evidence.

**`@rice-solar-physics` is rejected as an affiliation.** The live Zenodo lineage lists it as Will
Barnes's affiliation on all five records, but it is a GitHub organisation handle that the
GitHub–Zenodo integration copied from a profile field, not an institution, and the form asks for the
"Complete name without acronyms".

### 7. Software Name (MANDATORY)
**Value:** hissw

Carried over from the existing HSSI record and confirmed at the pinned revision by `setup.cfg`
(`name = hissw`), by the PyPI project name, and by `mkdocs.yml` (`site_name: hissw`). The README and
docs headline styles it "hiss(w)" and gloss it as "*hiss* (like a snake) + SSW"; that is
presentation, not the package name, and the lower-case `hissw` is correct.

### 8. Description (MANDATORY)
**Value:**

> Seamlessly integrate SSWIDL code into your Python workflow. The SolarSoftware (SSW) stack contains
> nearly every piece of software a solar physicist needs. hissw is a lightweight Python package that
> allows you to write IDL scripts (either inline or in a separate file) which use your installed SSW
> packages and return the results to your local Python namespace. hissw uses Jinja2 templates to
> generate SSW startup scripts and then runs your IDL code using subprocess. You can also use Jinja
> syntax to inject arguments from Python into IDL. The results are then saved to a file and then
> loaded back in using scipy.io.readsav().

This is the description HSSI already held, with one word restored. Everything after the first
sentence is a lightly-cleaned rendering of the opening of `docs/index.md`, and that editing is good
and is preserved: the source's parenthetical asides (it calls hissw "a (*VERY*) lightweight (~1
file) Python package" and `scipy.io`'s `readsav()` "amazing") and its markdown links have been
removed to give a catalogue-appropriate paragraph. No attempt is made to re-word it.

**The one change is the leading adverb.** The author's own one-line summary, in `setup.cfg` at the
pinned revision and on PyPI, is "Seamlessly integrate SSWIDL code into your Python workflow". Before
this refresh the stored description opened with that sentence word for word except that
"Seamlessly" was absent, which reads as a transcription loss rather than an editorial choice.
Restoring it makes the opening a faithful quotation of the author, and it is the only alteration to
a field whose wording is otherwise left exactly as a previous curator set it.

### 9. Concise Description (OPTIONAL)
**Value:** Easily integrate SSWIDL scripts into your Python workflow via Jinja templates

Carried over from the existing HSSI record. Its source is the PyHC community registry
(`_data/projects.yml`), whose hissw entry carries exactly this string as its `description` — PyHC
metadata is community-curated and takes priority over auto-extracted text. It is 77 characters, well
under the 200-character limit, and it names the three things that distinguish hissw (SSWIDL, Python,
Jinja). No change.

The README's own one-liner, "Easily integrate SSWIDL into your Python workflows.", was considered as
an alternative and rejected: it is nearly the same sentence but omits the Jinja templating, which is
the mechanism a prospective user most needs to know about.

### 10. Publication Date (RECOMMENDED)
**Value:** 2017-01-25

Carried over from the existing HSSI record and now properly grounded. This is the UTC date on which
the repository was created and the code first became public: the GitHub API reports `created_at:
2017-01-25T03:19:52Z`, and the first commit on the pinned lineage,
`564488a1434ea07e0b809d184fefadbc51290660` ("Initial commit"), is dated `2017-01-24 21:19:53 -0600`,
which is `2017-01-25 03:19:53Z`. The one-day discrepancy between the local-time commit stamp and the
stored value is a timezone artifact, not an error — noted here so a future agent reading `git log`
does not "correct" it to 2017-01-24.

**Alternatives considered.** The first tagged release (v1.0, 2018-09-12) and the first PyPI upload
(1.0, 2018-09-12T06:38:27Z) are both defensible readings of the field, which the form defines as
"Date of first broadcast/publication." They are rejected in favour of repository creation because
the form says of this field "Used for the initial version of the software.", and hissw was a
working, publicly readable package from January 2017 — the third and fourth commits, 28.6 hours
after the first (`2017-01-26 01:57:00 -0600`, which is two calendar days on from the initial
commit's local date), are "working package; added all templates and renderers; interface could be a
bit easier to use" and "setup for packaging". The 2018 date marks first *packaging*, not first
publication.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Carried over from the existing HSSI record and correct under the form's rule that Zenodo is the
publisher "For software where a DOI has been obtained through Zenodo (e.g., GitHub-Zenodo
workflow)". The workflow is confirmed rather than assumed: every record in both concept lineages
carries an `isSupplementTo` relation pointing at `https://github.com/wtbarnes/hissw/tree/<tag>`,
which is the relation the GitHub–Zenodo integration writes and which a manual deposit would not
have.

### 12. Version (RECOMMENDED)
- **Version Number:** v2.3
- **Version Date:** 2022-11-23
- **Version Description:** Add filter to force preservation of precision in floating point values
- **Version PID:** https://doi.org/10.5281/zenodo.7352323

The number, date and PID are carried over from the existing HSSI record and each independently
reconfirmed; the description fills a gap, as the stored version carried no description before this
refresh.

- **v2.3 is still the latest release.** The PyPI JSON API reports `version: 2.3` with seven releases
  matching the repository's seven tags. (The PyPI JSON endpoint is the authoritative check here: the
  HTML project page returns 200 even for packages that do not exist.) The `v2.3` form is preferred
  over PyPI's normalised `2.3` because it matches the git tag and the Zenodo title `wtbarnes/hissw:
  v2.3`.
- **The v2.3 tag is on the pinned lineage.** `git rev-list -n1 v2.3` gives
  `328607198bd9923bdc6e92e7ebca9f37950c4e1f`, `git merge-base --is-ancestor` confirms it is an
  ancestor of the pin, and it is the pin's immediate parent — exactly one commit separates the
  catalogued release from the current tip of `main`.
- **2022-11-23 is the release date, not the tag date.** The tag commit is dated `2022-11-22 14:40:16
  -0500`; the release event is a day later, and two independent records agree on that date while
  falling less than half a minute apart, which is strong corroboration that they are recording the
  same event rather than two loosely related ones: Zenodo record `7352323` has `publication_date:
  2022-11-23` and `created: 2022-11-23T18:20:27Z`, and PyPI's 2.3 sdist uploaded at
  `2022-11-23T18:20:51Z`, 24 seconds later. The form asks for the date the version was released, so
  2022-11-23 stands.
- **The description is the sole change in the release**, taken from the GitHub release notes as
  mirrored in the Zenodo record's description. That section contains a single bullet, "Add filter to
  force preservation of precision in floating point values by @wtbarnes in
  https://github.com/wtbarnes/hissw/pull/32"; the recorded description is that sentence with the
  contributor-and-pull-request trailer dropped, since the trailer is release-note formatting rather
  than part of the change description. The change is the `force_double_precision_filter` now present
  in `hissw/filters.py` and documented under "A Note on Preserving Precision between Python and IDL"
  in `docs/index.md`.

**Note on how this field renders.** HSSI's view API returns the version name-prefixed, as `hissw -
v2.3`; the stored value is `v2.3`. The rendered string must never be copied into a value.

**A retired earlier reading, recorded so it is not reintroduced.** An earlier extraction listed both
v2.3 and v2.0 as versions, because the README's "Citing `hissw`" BibTeX block cites v2.0
(`10.5281/zenodo.6640421`) as the preferred citation. That README block is simply out of date — the
author has not refreshed it since the v2.0 release — and the field asks for the version of the
software instance, which is v2.3. The v2.0 DOI belongs nowhere in this record; it is worth knowing
about only because the two papers in Field 27 cite different versions of hissw, one each.

### 13. Programming Language (RECOMMENDED)
**Values:** IDL, Python 3.x

Carried over from the existing HSSI record and confirmed. Python 3 is the implementation language
(`python_requires = >=3.6` in `setup.cfg`; `docs/index.md` states "* Python-3 only"), and IDL is not
incidental — `hissw/templates/parent.pro` and `hissw/templates/procedure.pro` are IDL source shipped
in the package, and generating and executing IDL is the point of the software.

`Other` was considered for `hissw/templates/startup.sh`, a tcsh script, and rejected: the form asks
for "the most important languages" and explicitly says the list "is not meant to be an exhaustive
list". A generated shell wrapper does not rise to that.

### 14. Reference Publication (OPTIONAL)
**Value:** Not found — documented omission.

hissw has no paper describing it. This is a negative result that was tested rather than assumed,
because a repository-name-keyed search alone is structurally blind to a manually-deposited artifact:

- The README's "Citing `hissw`" section supplies a **software** BibTeX entry (`@software{...}`,
  publisher Zenodo) — the author's chosen citation is the code archive, not a paper.
- **Title-keyed:** an ADS/SciX `title:"hissw"` search returns only the two Zenodo software records
  (`2022zndo...7352323B`, `2022zndo...6640421B`). A Zenodo full-text search for `hissw` returns only
  the latest record of each of the two concept lineages.
- **Creator-keyed** (the check that does not depend on the software's name): Zenodo searches on Will
  Barnes's ORCID `0000-0001-9642-6089` and on the creator name "Barnes, Will" return his other
  software and conference deposits — fiasco, aiapy, EBTEL, XRTpy, sunpy, EISPAC, ebtelplusplus,
  numerous posters — and, for hissw, only the software records already known.
- **Redirect-keyed:** probes of plausible predecessor repository names (`scivision/hissw`,
  `rice-solar-physics/hissw`, `wtbarnes/hiss`) all 404 without redirecting, so there is no earlier
  project identity carrying a paper.

There is no JOSS submission, no `paper.md`, and no `paper/` directory at the pinned revision.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

**HSSI held no licence value for this field before this refresh**; the value is derived here. The
evidence agrees across the repository itself, its packaging metadata, GitHub's own licence
detection, and the retired Zenodo lineage. Exactly one source dissents, and it is named below:

- `LICENSE` at the pinned revision is the verbatim MIT text, opening "MIT License" / "Copyright (c)
  2017 Will Barnes".
- `setup.cfg` declares the classifier `License :: OSI Approved :: MIT License`, and PyPI reports the
  same classifier for the 2.3 release.
- The GitHub API reports the repository licence as SPDX `MIT`.
- The retired Zenodo lineage records `license: {"id": "mit-license"}` on both v1.0 and v1.1.

`MIT License` is the exact controlled-vocabulary row name, and `https://spdx.org/licenses/MIT` is
the URL that row carries.

**The conflicting source is named so it is not mistaken for new information later.** Every record on
the *live* Zenodo lineage (v1.2 through v2.3) declares `license: {"id": "other-open"}`. That is a
Zenodo-side error introduced when the deposit moved to the new lineage, and it must not be
transcribed into this field — `Other` is a real row in the controlled vocabulary, so the wrong value
would be accepted without complaint. The repository's own `LICENSE` governs.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:** idl, idl save, python, solar, solar physics, solarsoft, ssw, sswidl, sun, wrapper

Nine of the ten were already on the record and are carried over unchanged; the tenth replaces a
malformed value. (HSSI stores keywords lower-case and title-cases them for display, so the stored
strings — not the rendered `Idl`, `Solar Soft` — are what is recorded here.) Each keep is justified
from the searcher's side: would someone type this, and would finding hissw under it make sense?

- **`idl`, `sswidl`, `ssw`** — the three terms that actually identify this package. `ssw` and
  `sswidl` are not redundant spellings of one another: `ssw` is the library abbreviation used
  throughout the docs and the `ssw_packages` API, `sswidl` is the executable hissw invokes and the
  form in which people write about running SSW code. Someone typing either should reach hissw.
- **`solar`, `sun`, `solar physics`** — three broad solar terms, all three of them the author's own
  (`setup.cfg` lists `solar`, `sun`, `solar-physics`). HSSI's space-separated `solar physics` is
  preferred over the source's hyphenated `solar-physics` because the hyphen is a packaging-metadata
  convention and the space is what a person types.
- **`wrapper`, `idl save`** — both are PyHC-curated (the registry entry's keywords are `solar`,
  `general`, `wrapper`, `idl_save`), and PyHC is the most trustworthy source in the cascade.
  `wrapper` is not a generic term here: it names a narrow kind of package that hissw emphatically
  is, and it is a plausible search term for someone looking for exactly this kind of tool. `idl
  save` names the concrete interchange artifact. (PyHC's fourth keyword, `general`, is correctly not
  stored — it carries no information.)
- **`python`** — kept. It is a weak keyword in the sense that it discriminates little, but the test
  applied throughout this dossier is whether a searcher is helped or annoyed, and `python` is
  neither: it is true, it is unsurprising on the page, and removing it would be a tidiness change
  with no user-facing benefit. Field 13 already records Python 3.x, but that is not a reason to
  strip a truthful tag.

**`solarsoft` stands in place of the malformed `solar soft`.** The two-word form the record held
before this refresh matches no source and no usage: the library's own name is one word — LMSAL
publishes it as SolarSoft, `README.md` says "[Solarsoft library]", HSSI's own catalogue entry for
the library is named `SolarSoft` — and the author's keyword in `setup.cfg` and on PyPI is
`solarsoft`. Nobody searching for this library types a space. Since HSSI's keyword search matches on
the stored string, "solar soft" made hissw invisible to the obvious query while contributing nothing
that `ssw` and `sswidl` do not already cover. The Keyword vocabulary held no `solarsoft` row before
this refresh, but Keywords is the one open vocabulary in the form and a missing row is created on
write, so the repair is safe. *The counter-evidence, recorded in fairness: the repository's GitHub
topics are `idl`, `python`, `solar-physics`, `solar-soft` — the author did hyphenate it there. Two
of his three keyword lists say one word, and the one-word form is the library's actual name.*

**Considered and not added.** `heliophysics` and similar catalogue-wide terms were rejected as
uninformative; `jinja2` and `templating` were rejected because a user does not search for a solar
tool by its templating engine, and Field 30 already records the interoperability that matters.

### 17. Data Sources (OPTIONAL)
**Value:** Not applicable — evidenced empty.

hissw retrieves no data. There is no HTTP, FTP, or archive-query code anywhere in `hissw/`; the only
I/O it performs is writing generated scripts into a `tempfile.TemporaryDirectory()` and reading back
the IDL save file that IDL wrote there. Every value in the vocabulary — AMDA, CDAWeb, das2, FTP/FTPS
Directories, GFZ, HAPI, HTTP/HTTPS Directories, Madrigal, Observatory/Mission-specific, OMNIWeb,
S3/Cloud-aware, SSCWeb, TAP, The Virtual Solar Observatory., VirES, WDC — names a source hissw does
not touch, and `Other` would assert a source that does not exist. Whatever data a user's IDL script
loads, it loads through SolarSoft, whose own catalogue record carries those capabilities.

This is the same finding that removes `Data Access and Retrieval` from Field 4; the two fields are
now consistent, where previously they contradicted each other.

### 18. Input File Formats (RECOMMENDED)
**Value:** IDL.sav

Carried over from the existing HSSI record. `Environment.run` ends with `results =
readsav(save_filename)` (`hissw/environment.py`), reading the IDL save file produced by the
templated `save,...,filename='...'` statement in `hissw/templates/procedure.pro`. This is the only
data format hissw itself parses.

The `.pro` script file that `render_script` may read from disk is **not** listed: it is program
source supplied by the user, not a data input, and `ascii` would misdescribe it as a data format the
software supports.

### 19. Output File Formats (RECOMMENDED)
**Value:** IDL.sav

Carried over from the existing HSSI record. The IDL save file is the artifact hissw's pipeline
produces and consumes — hissw templates the `save` statement that creates it and then reads it back.

The `.pro` and `.sh` files hissw writes into its temporary directory are **not** listed: they are
transient generated code, deleted when the `TemporaryDirectory` context exits, not data products a
user receives. Any other output format a user ends up with is written by their own IDL, not by
hissw.

### 20. Operating System (RECOMMENDED)
**Values:** Linux, Mac

Carried over from the existing HSSI record, and stated by the author rather than inferred.
`docs/index.md` warns: "Relies on executing shell commands with the `subprocess` module. I've only
tested this on Linux and macOS. **Windows users may encounter difficulties.**" `README.md` repeats
it: "**Note: hissw relies on executing several shell commands. This has not been tested on
Windows.**" The only CI runner in `.github/workflows/` is `ubuntu-latest`.

`Windows` is rejected — the form asks for systems the software "can successfully be installed on",
and the author explicitly disclaims it. `Operating System Independent` is rejected for the same
reason: the templated startup script has a `#!/bin/tcsh` shebang and sources
`$SSW/gen/setup/setup.ssw`, so the design is Unix-shell-bound.

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

Carried over from the existing HSSI record. hissw is pure Python with no compiled extension, no
architecture-specific code path and no binary artifact; `setup.cfg` declares no platform constraint.
Any architecture limitation a user meets comes from their IDL installation, which is not part of
this package.

### 22. Related Phenomena (OPTIONAL)
**Value:** None — evidenced empty.

**Four values stood on the record before this refresh and none of them survives scrutiny:** Coronal
Heating, Solar Corona, Solar Flares and X-ray emission. They had been justified as "typical SSW use
cases", with the acknowledgement that the specific phenomena depend on which SSW packages the user
loads. That is a description of SolarSoft's reach, not of hissw's, and it is the same inheritance
that had put `Data Access and Retrieval` in Field 4.

**The decisive evidence is the arbitrariness of the subset.** hissw implements no
phenomenon-specific science whatsoever — there is no flare detection, no coronal model, no spectral
inversion, no physical constant in any of its modules. Its relationship to *every* solar phenomenon
is identical and entirely indirect: whatever SSW package a user chooses to load. So there is no fact
about hissw that explains why it is tagged Solar Flares but not Coronal Mass Ejections, or X-ray
emission but not Solar Wind. Any principled selection is therefore all-or-nothing, and "all" is
plainly wrong (`Geomagnetic Storms` is in the vocabulary and hissw is not geomagnetic-storm
software).

**From the searcher's side.** Someone filtering on `Solar Flares` is looking for flare software —
detection, modelling, flare-data analysis — and a Jinja templating bridge is noise in that list.
Meanwhile, someone filtering on `Coronal Mass Ejections` missed hissw for no reason at all. That
tagging gave a user an unhelpful hit in four filters and an unexplained miss in two; leaving the
field empty fixes both sides of it.

**Why this does not contradict Field 5.** The two fields ask different questions and their
vocabularies differ in the way that matters. Field 5 asks what physical region the software is
*commonly used or intended for*, and the vocabulary offers `Solar Environment`, a value that means
exactly "solar, region unspecified" — precisely the claim the evidence supports. Field 22 asks what
phenomena the software supports science functionality for, and every one of its seven values is a
*specific* phenomenon; there is no "solar generally" option. Selecting six of the seven to mean
"solar" would only restate Field 5 while diluting six real filters. The same rule — never assert
more specificity than the evidence carries — produces a value in one field and silence in the other.

### 23. Development Status (RECOMMENDED)
**Value:** Inactive

**HSSI held no development-status value for this field before this refresh**; the value is derived
here from the repostatus.org definitions the vocabulary carries.

The applicable definition, quoted exactly from the `Inactive` row: *"The project has reached a
stable, usable state but is no longer being actively developed; support/maintenance will be provided
as time allows."* Both halves are satisfied.

- **Stable and usable.** `setup.cfg` declares `Development Status :: 5 - Production/Stable`; seven
  releases are on PyPI; the package has a test suite covering filters, script rendering, error
  handling and a live SSW round-trip.
- **No longer actively developed.** The last commit on `main` is the pinned revision, made at
  `2024-02-06T01:38:09Z`. That single instant renders on two calendars — its committer timestamp is
  `2024-02-05 20:38:09 -05:00`, so `git log` in a US Eastern locale shows it a calendar day earlier
  — the same local-versus-UTC discrepancy Field 10 reconciles for the first commit. The last release
  is v2.3, tagged `2022-11-22` and published `2022-11-23`. Nearly four years have passed without a
  release and more than two without a commit to the default branch.

The two neighbouring values were tested against their own definitions and rejected:

- **`Active`** — *"The project has reached a stable, usable state and is being actively developed."*
  The second clause fails on the commit and release record above. (An earlier extraction chose
  `Active` partly on a reported last commit of 2024-12-26; that date is the GitHub API's
  `updated_at`, a repository-metadata timestamp, not a commit date. The last push to any branch is
  `pushed_at: 2024-10-02T02:10:44Z`.)
- **`Unsupported`** — *"The project has reached a stable, usable state but the author(s) have ceased
  all work on it. A new maintainer may be desired."* Both sentences fail. Work has not ceased:
  commit `e55a5ebbf7469a9f2e8db2d6fcc2188c0b6aa585` (2024-10-01) on the `add-logging` branch merges
  `main` into an in-progress feature, i.e. the author was still developing hissw eight months after
  the last commit to `main`. And no maintainer is being sought: the repository is not archived
  (`archived: false`, `disabled: false`), has open issues, and carries no deprecation or
  seeking-maintainer notice. `Unsupported` describes a project whose authors have ceased all work on
  it — the pattern an archived, read-only repository fits — whereas hissw's repository is neither
  archived nor closed.

### 24. Documentation (RECOMMENDED)
**Value:** https://wtbarnes.github.io/hissw/

Carried over from the existing HSSI record and reachable, serving the documentation site itself
(`<title>hissw</title>`) rather than a redirect or a placeholder. It is the URL declared in
`setup.cfg` under `project_urls` (`Documentation =
https://wtbarnes.github.io/hissw/`), in `mkdocs.yml` (`site_url:
'https://wtbarnes.github.io/hissw'`), in the PyHC registry, and as the GitHub repository homepage.
The site is built by the `Deploy Docs` workflow from `docs/` and includes installation instructions,
so it satisfies the form's requirement for a link that covers installation.

### 25. Funder (OPTIONAL)
**Value:** Not found — documented omission.

No funding attribution exists to record. A text sweep of the entire tree at the pinned revision for
funding, acknowledgement, grant and agency terms returns exactly one hit, and it is the MIT
licence's phrase "Permission is hereby granted, free of charge". There is no acknowledgements
section in the README or the documentation, and no `grants` entry on any of the seven Zenodo records
across both concept lineages.

This absence is unsurprising for a personal utility package rather than a mission or grant
deliverable, and it is not an extraction gap. Note that the funding acknowledged in the two papers
of Field 27 funded *those studies*, not hissw, and must not be imported here.

### 26. Award Title (OPTIONAL)
**Value:** Not found — documented omission.

Follows directly from Field 25: with no funder identified anywhere in the repository, the Zenodo
records, or the package metadata, there is no award to record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.3847/1538-4357/ad37f7
- https://doi.org/10.3847/1538-4357/ad3424

**HSSI held no related publications for this field before this refresh.** These are the two refereed
papers that cite hissw, both published in *The Astrophysical Journal* in 2024 and both citing it as
"Barnes, W., & Chen, B." with its Zenodo DOI.

- **Duncan et al. 2024, ApJ 966, 197** — "Thermal Evolution of an Active Region Through Quiet and
  Flaring Phases as Observed by NuSTAR, XRT, and AIA". This is substantive methodological use, not a
  courtesy citation. Its methods section states: "The hissw Python package was used to incorporate
  the functionality of these and other SSWIDL libraries while performing analysis in Python" (quoted
  from the arXiv preprint, arXiv:2312.05109v1), in the context of obtaining AIA temperature
  responses via `aia_get_response.pro`. It cites hissw v2.0, `10.5281/zenodo.6640421`.
- **Zhu et al. 2024, ApJ 966, 122** — "Spectroscopic Observations of the Solar Corona during the
  2017 August 21 Total Solar Eclipse: Comparison of Spectral Line Widths and Doppler Shifts between
  Open and Closed Magnetic Structures". hissw appears in the paper's software list alongside
  SolarSoft, EISPAC, SunPy and CHIANTI, citing v2.3, `10.5281/zenodo.7352323`. This is a
  software-credit citation rather than a described method, and it is included on that footing.

Together these are the clearest available demonstration that hissw is used in published science, and
they show a prospective user what it is used *for* — pulling SSWIDL instrument-response and
data-reduction routines into a Python analysis. That is a genuine benefit on the software's page.

**Completeness caveat.** These two were found by ADS/SciX full-text search (`full:"hissw"`, and
`ack:"hissw"` which returns the same two). The same search also returns the hissw Zenodo software
records themselves and one 2012 arXiv preprint on Bayesian phase measurement that has no connection
to this package — a string-match false positive, recorded so it is not investigated again. ADS
full-text indexing does not cover every journal, so two should be read as a floor rather than a
proven ceiling.

### 28. Related Datasets (OPTIONAL)
**Value:** Not applicable — evidenced empty.

hissw ships no data, reads no named dataset and is bound to no data product. The IDL save file it
reads back is produced during the same call by the user's own script. There is no dataset a user of
hissw is expected to obtain, so there is nothing to link.

### 29. Related Software (OPTIONAL)
**Value:** None — evidenced empty.

Every candidate was assessed, and each is either better placed in Field 30 or excluded by the
generic-infrastructure rule. Nothing remains.

- **SolarSoft** is the obvious candidate and it does qualify as an important, domain-specific
  dependency — but Field 29 is scoped to software that "does not necessarily link together (which
  would be 'interoperable software')", and hissw and SolarSoft link together as tightly as two
  packages can. It is recorded in Field 30 instead. Listing the same URL in both fields would show a
  user the same link twice.
- **IDL** is rejected. It is the commercial runtime hissw shells out to, not heliophysics software
  and not a catalogue item; a user reading "Related Software: IDL" learns nothing they did not learn
  from Field 13.
- **The official Python-to-IDL bridge** is the strongest rejected candidate and is recorded here in
  full so the case does not have to be rebuilt. `docs/index.md` presents it as the alternative to
  hissw: "If you're interested in something more complicated (and harder to install), you may want
  to check out the more official [Python-to-IDL
  bridge](https://www.harrisgeospatial.com/docs/Python.html)." That is exactly Field 29's "performs
  similar tasks" relationship. It is rejected on three grounds: the URL in the documentation is dead
  (`harrisgeospatial.com` no longer resolves at all, following the vendor's rebranding through
  L3Harris to NV5); the successor page `https://www.nv5geospatialsoftware.com/docs/Python.html` is
  live but appears nowhere in the repository, so recording it would assert a link the project never
  made; and the bridge is a feature of the same proprietary IDL runtime rejected in the previous
  point, which makes admitting it inconsistent with excluding IDL itself.
- **SunPy, Astropy and ChiantiPy as *alternatives*** are rejected. `docs/index.md` mentions all
  three in one sentence — "While libraries like [Astropy](http://www.astropy.org/),
  [SunPy](http://sunpy.org/), and [ChiantiPy](https://github.com/chianti-atomic/ChiantiPy) provide
  Python equivalents to many of these IDL packages, there's still a lot of functionality only
  available in SSW." — but read carefully, that sentence says they are equivalents to the *SSW
  packages*, not to hissw. It is ecosystem context, not a claim that any of them performs hissw's
  task, and none of them does — running SSWIDL from Python is not something SunPy, Astropy or
  ChiantiPy attempt. (Astropy does appear in Field 30, on entirely different and much more specific
  evidence; ChiantiPy and SunPy have no such evidence, which is why they appear in neither field.)
- **jinja2 and scipy** (`install_requires`), **numpy** (imported at module scope in
  `hissw/filters.py`, and an undeclared runtime dependency — `install_requires` lists only jinja2
  and scipy), and the **pytest / mkdocs / mkdocs-material / setuptools_scm** development stack are
  all excluded by rule, not by preference. They are generic infrastructure — templating, arrays,
  numerics, testing, docs building, packaging — equally at home in a web application or a finance
  model, and listing them would say nothing that is not equally true of most of the catalogue. This
  exclusion is the same rule Field 30 applies; a package excluded there does not land here by
  default.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://www.lmsal.com/solarsoft/ — SolarSoft
- https://github.com/astropy/astropy — Astropy

**HSSI held no interoperable software for this field before this refresh.** Both entries are
in-catalogue software, and each URL is the value HSSI's own entry for that package carries as its
code repository, so both bind to the existing catalogue items rather than minting new ones.

**SolarSoft.** This is the relationship hissw exists for, and it is the textbook case of the
qualifying pattern the field names — "a cross-language bridge to a named domain tool (an IDL SPEDAS
or MATLAB interface)". The exchange is concrete and is hissw's entire public behaviour:
`Environment` takes `ssw_packages` and `ssw_paths` arguments, `shell_script()` sets `SSW`,
`SSW_INSTR` and `IDL_DIR` and sources `$SSW/gen/setup/setup.ssw`, `command_script()` emits
`ssw_path,/<paths>` into the IDL session, and the `executable` property selects `sswidl` whenever an
SSW tree is configured. `README.md` states the requirement outright: "Additionally, you'll need a
local install of IDL and the [Solarsoft library](http://www.lmsal.com/solarsoft/)." Decided from the
searcher's side, this is the clearest gain in the whole refresh: a user on the SolarSoft page asking
what software relates to it should find the tool that lets them call SSW from Python, and a user on
the hissw page should be told which library it bridges to.

**Astropy.** Admitted on the Tier B standard — a *specific documented exchange*, not dependency
presence — and the evidence is specific on four surfaces. hissw's `units_filter`
(`hissw/filters.py`) consumes another package's data model directly: it requires an
`astropy.units.Quantity`, raises `u.UnitsError` if given anything else, and returns
`quantity.to_value(unit)`. `Environment.__init__` registers it by default on every instance as the
`to_unit` Jinja filter, so it is part of the public API rather than an internal helper. `setup.cfg`
provides a dedicated `astropy` extra. `docs/examples/aia_example.md` works the exchange end to end,
passing `np.linspace(0.1, 100, 1000) * u.MK` through `{{ temperature | to_unit('K') | log10 | list
}}` into an IDL script, and the test suite exercises it repeatedly, including `test_units_filter`,
`test_units_filter_exception`, `test_units_filter_array` and
`test_force_double_precision_filter_with_quantity`. Notably astropy is a deliberate *non*-dependency
— `hissw/filters.py` imports it inside the function with the comment "# Avoid astropy as a hard
dependency" — which is what an interoperability affordance looks like as distinct from a dependency.
On the user's side: telling a reader that hissw accepts Quantities is useful, actionable information
about how to use it.

**Rejected here for completeness:** jinja2, scipy and numpy — Tier A generic infrastructure,
excluded by rule; being a dependency is not interoperability, and "it depends on scipy" is true of
much of the catalogue. SunPy and ChiantiPy — no adapter, no shared data model, no example, no test;
the single documentation sentence that names them is a contrast with SSW rather than a relationship
with hissw (see Field 29). Blanket claims of the form "part of the standard scientific Python
ecosystem" or "a PyHC member, so it interoperates with PyHC packages" were not used and are never
sufficient.

### 31. Related Instruments (OPTIONAL)
**Value:** None — evidenced empty.

hissw is instrument-agnostic by construction. It contains no instrument-specific parser,
calibration, response function or convention; whatever instrument a user works with, they work with
it in their own IDL through SolarSoft.

**The AIA appearances were assessed and do not change this.** At the pinned revision SDO/AIA appears
in three roles and no others: as an example value for the `ssw_packages` argument in the
`Environment` docstring ("List of SSW packages to load, e.g. 'sdo/aia', 'chianti'"), as the subject
of `docs/examples/aia_example.md` and its navigation entry in `mkdocs.yml`, and in the `ssw_env`
test fixture and `test_aia_response_functions`. All three fall in the relevance gate's excluded
categories: the docstring line and the example page are tutorial/demonstration name-drops, and the
test is a smoke test that uses a convenient real SSW routine (`aia_get_response`) to prove the SSW
path works. The AIA-specific logic in each case is IDL supplied by the example or the test, not code
hissw ships.

Decided from the searcher's side: someone on the AIA page asking what software supports this
instrument expects aiapy, sunpy and AIA preparation tools. hissw knows nothing about AIA and would
be out of place there.

**This is a relevance decision, not a resolution failure** — worth stating precisely, because the
distinction matters for a future agent. The instrument does resolve cleanly: the controlled
vocabulary contains `Atmospheric Imaging Assembly`, identifier
`https://spase-metadata.org/SMWG/Instrument/SDO/AIA`. It is deliberately not recorded.

### 32. Related Observatories (OPTIONAL)
**Value:** None — evidenced empty.

The same reasoning as Field 31 applies at the mission level. hissw is not purpose-built for any
mission, implements no mission's data conventions, and processes no mission's data products; SDO
appears only through the `'sdo/aia'` example, the AIA example page and the AIA test. A user on the
Solar Dynamics Observatory page asking for related software would not expect a Python-to-IDL bridge.

As with Field 31, the omission is a relevance judgement rather than an unresolved lookup: the
observatory row exists — `Solar Dynamics Observatory`,
`https://spase-metadata.org/SMWG/Observatory/SDO` — and is deliberately not used. Should this field
ever be filled, no entry may be recorded without an `https://spase-metadata.org/` identifier; a bare
name creates a new identifierless row.

### 33. Logo (OPTIONAL)
**Value:** Not found — documented omission.

hissw has no logo. Every candidate was located, fetched, and looked at:

- **`docs/images/ex1.png`, `ex2.png`, `exAIA.png`** — the only images in the repository at the
  pinned revision. All three are 1280×960 matplotlib figures reproducing the documentation's worked
  examples: `ex1` and `ex2` are the viridis upper-triangular masks from `simple_example.md`, and
  `exAIA` is the six-channel AIA temperature-response plot from `aia_example.md`. They are example
  output, not branding, and they are referenced in the docs as figures.
- **`assets/images/favicon.png` on the `gh-pages` branch** — a 48×48 PNG that is the stock
  mkdocs-material theme favicon, not a project asset.
- **`mkdocs.yml`** sets `theme.icon.logo: 'fontawesome/solid/code'`, a generic Font Awesome glyph
  chosen from the theme's icon set rather than a hissw mark.
- **The documentation site** at `https://wtbarnes.github.io/hissw/` serves no images at all on its
  landing page.
- **The PyHC registry entry** for hissw has no `logo:` field, unlike many entries in the same file.

The nearest thing hissw has to a mark is the README's emoji headline, ":snake: :sunny: hiss(w)",
which is text and cannot be a Field 33 URL. No logo is invented; the omission is the correct
outcome.

