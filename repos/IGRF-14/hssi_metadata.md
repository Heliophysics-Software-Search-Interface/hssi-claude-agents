# HSSI Metadata Extraction Results

**HSSI Software ID:** 6e225ee4-8f52-4441-a7e9-0ed2ca804067
**Repository:** https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field
**Source Revision:** Zenodo version record 14218973 (`https://doi.org/10.5281/zenodo.14218973`), the latest version under concept DOI `10.5281/zenodo.14012302`; record metadata last modified upstream 2026-07-03. NCEI product page retrieved 2026-08-06. There is no git SHA — see the scope note below.
**Extraction Date:** 2026-08-06
**Validation Date:** 2026-08-06
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

This entry is the **IGRF-14 model coefficient release published on Zenodo**, not a source-code
project. That identity is fixed by the record's own anchors: the persistent identifier is the Zenodo
concept DOI, the publisher is Zenodo, the Zenodo `resource_type` is `Model`, and the licence is the
Zenodo record's CC-BY-4.0. The release consists of exactly three data files — `igrf14coeffs.txt`,
`IGRF14coeffs.xlsx` and `IGRF14.shc` — and contains no source code, build configuration, test suite
or package manifest.

Consequently **there is no version-controlled repository to read**, and Field 3 holds an
authoritative landing page rather than a git remote (see Field 3). Evidence throughout this file is
drawn from the Zenodo/DataCite records for the release, the NOAA/NCEI product page, the peer-reviewed
IGRF-14 papers, and the release artifacts themselves.

**The synthesis programs distributed from the NCEI page are deliberately out of scope** for this
entry. That single decision determines Fields 13, 18 and 19, and is set out in full under Field 13
because it is the field where its consequences are least obvious. Read that note before proposing
values for any of those three fields.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not part of the software's descriptive metadata; supplied by whoever transmits the record.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.14012302

Zenodo **concept** DOI, covering all versions — which is what this field asks for. Confirmed against
the Zenodo and DataCite records for the release: record 14218973 reports
`conceptdoi: 10.5281/zenodo.14012302` and carries an `IsVersionOf` relation to it.

The version-specific DOI (`https://doi.org/10.5281/zenodo.14218973`) deliberately does **not** go
here — it belongs in Field 12 as the Version PID, where it is recorded.

### 3. Code Repository (MANDATORY)
https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field

**There is no authoritative Git repository for the IGRF-14 release; this NCEI product page is the
right value for the field, and it should not be replaced with a repository URL.** The reasoning, so
it does not have to be rediscovered:

- The release is a set of coefficient files with no version-control history. Nothing exists to clone.
- `IAGA-VMOD/IGRF14eval` is *evaluation* software for the candidate models that fed the release, not
  the release itself. Its own README points readers wanting "the IGRF-14 release itself" to
  `https://doi.org/10.5281/zenodo.14012302` and to this NCEI page. The release record classes it as
  supplementary (`IsSupplementedBy` → `10.5281/zenodo.14205633`), and the eval record reciprocates
  with `isSupplementTo` → the release concept DOI. It is therefore recorded in Field 29, not here.
- `IAGA-VMOD/ppigrf` is an independent implementation that *consumes* IGRF coefficients, not the
  release. Also recorded in Field 29.

This NCEI page is the authoritative access point: it is the URL the release's own description directs
readers to ("For more information, see …"), it is maintained by the NOAA World Data System alongside
the IAGA V-MOD working group, and it distributes the release's own artifacts. The two coefficient
files it distributes are the release's own, matching the Zenodo files by MD5 — `igrf14coeffs.txt` at
`md5:3606931c15c9234d9ba8e2e91b729cb0` and `IGRF14coeffs.xlsx` at
`md5:dd71a0f748f047704997743475c3209d`. Those are the two formats the page's coefficient download
links offer; the release's `IGRF14.shc` is published on the Zenodo record. (A file named `IGRF14.SHC`
is also bundled inside the NCEI-hosted `pyIGRF14.zip`, but it is a smaller, different file than the
release's `IGRF14.shc` and must not be treated as a copy of it.)

A website-only source is a legitimate outcome for a record of this kind. Where that leaves a field
genuinely undiscoverable, this file records a documented omission rather than a substitute value.

### 4. Software Functionality (MANDATORY)
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Forecasting

**`Models and Simulations`** — the parent of both children below. This field's subcategories do not
imply their parent: where a child applies, the parent belongs in the list alongside it. A value set
naming only `Models and Simulations: Empirical` would therefore be incomplete for this model, and the
parent is not optional decoration.

**`Models and Simulations: Empirical`** — IGRF is a spherical-harmonic representation whose Gauss
coefficients are fitted to observations from satellites, magnetic observatories and surveys. The
coefficient file header states the model is expressed in "Schmidt semi-normalised spherical harmonic
coefficients, degree n=1,13". This is the archetypal empirical geophysical model and the
classification is unambiguous.

**`Models and Simulations: Forecasting`** — the release ships a genuinely *predictive* component, not
only a retrospective fit. The coefficient table's final column is the secular-variation model labelled
`SV 2025-30`, and the file header describes it as "degree n=1,8 nanoTesla/year for secular variation
(SV)". The official synthesis program's header calls it "The predictive secular-variation model" and
records that "the secular-variation model for 2025.0 to 2030.0 is non-definitive". This is why the
release, published in 2024, "covers the period from 1900 to 2030": coverage past 2025 is by forward
prediction. Forecasting is therefore a first-class function of the model, not an incidental property.

**Considered and rejected**, so these are not re-proposed:

- `Models and Simulations: Data Guided` — reserved for models driven by observational data *at run
  time* (data-derived boundary conditions, live inputs). IGRF-14 is a static, published fit; the
  observational basis is already expressed by `Empirical`, and adding this would double-count it.
- `Models and Simulations: Physics-Based` and `: First Principles` — the spherical-harmonic form
  follows from potential theory, so the temptation is real, but the coefficients are empirically
  fitted rather than derived from governing equations. `Empirical` is the precise label for a
  reference field of this kind, and adding a physics category would blur that distinction.
- `Models and Simulations: Theory`, `: MHD`, `: Mission-Specific`, `: ML/AI`,
  `: Observatory/Instrument Models`, `: Forward-Fitting`, `: Instrument Response`,
  `: Field-line Tracing` — none is implemented by or applicable to a published coefficient set.
- `Coordinate Transforms` (and its children, in particular `: Magnetospheric` and `: Ionospheric`) —
  the release performs no transforms. Geodetic↔geocentric conversion exists in the NCEI-hosted
  synthesis programs, which are out of scope (Field 13). Were those programs ever catalogued
  separately, `Coordinate Transforms` would belong to *their* records.
- `Data Processing and Analysis` and `Data Visualization` families — the release neither processes nor
  renders anything; it is the input such tools consume.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Ionosphere

Both regions rest on the release's own description, which states the model "is used widely in studies
of the Earth's deep interior, crust, ionosphere, and magnetosphere" — naming the magnetosphere and the
ionosphere explicitly. `Earth Ionosphere` is preferred over the broader `Earth Atmosphere` because the
field offers the specific term and the source names the specific region.

**Two of the four application areas the description names cannot be expressed in this vocabulary.**
This field offers no term for the Earth's deep interior, core, crust or lithosphere; its one interior
term, `Solar Interior`, is solar. Those two areas are instead carried by the keywords
`core field` and `crustal field` in Field 16. A future agent should not read their absence here as an
oversight.

**Considered and rejected:** `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`,
`Earth Magnetotail` and `Earth Magnetosheath`. IGRF-14 supplies the *internal* main field that serves
as the baseline throughout the magnetosphere rather than modelling any one subregion, and no source
consulted distinguishes among them. Selecting all four would be padding; selecting one would be a
guess. The general `Earth Magnetosphere` row states exactly what the sources support.
`Earth Thermosphere`, `Earth Auroral Subregion`, `Earth Atmosphere` and
`Earth Lower and Middle Atmosphere` were likewise rejected for want of any supporting statement in
the release description, the NCEI product page or the IGRF-14 papers.

### 6. Authors (MANDATORY)
- **Author:** International Association of Geomagnetism and Aeronomy
  - **Author Identifier:** https://ror.org/013ym9476
  - **Affiliation:** none

**This author is an organization, not a person.** DataCite records exactly one creator for the
release: `{"name": "International Association of Geomagnetism and Aeronomy", "nameType":
"Organizational", "nameIdentifiers": [{"nameIdentifier": "013ym9476", "nameIdentifierScheme":
"ROR"}]}`. The ROR record `https://ror.org/013ym9476` is active, typed `nonprofit`, located in
Strasbourg, France, and carries the English label "International Association of Geomagnetism and
Aeronomy" together with the acronyms `IAGA` and `AIGA`. The English label is used here because the
form asks for the complete name without acronyms; ROR's own display name is the French
"Association Internationale de Géomagnétisme et d’Aéronomie".

A ROR is the correct identifier for an organization author, which is why the ROR above is recorded
rather than any person identifier.

**No affiliation is recorded, deliberately.** DataCite gives `affiliation: []`, and an organization
credited as the author is not affiliated with anything further — attaching IAGA's own location or
parent body as an "affiliation" would invent a relationship the sources do not assert.

**The live author representation, and why it should be left as it stands.** This author is currently
recorded as a person rather than an organization, with the name divided so that "International
Association of Geomagnetism and" and "Aeronomy" occupy separate name parts. It carries the correct
IAGA ROR given above, and it reads intelligibly as "International Association of Geomagnetism and
Aeronomy". The division nonetheless does not reflect the correct semantics, which are a single
organization name carrying that ROR.

The difference is recorded here so that it is neither mistaken for extraction drift nor treated as a
value to adjust during a metadata refresh. The name belongs to a shared identity record that this
software only references, so putting it right is a separate question about that record — including what
else depends on it — and needs its own investigation before anything is altered. Absent that, the
representation described above is the correct thing to leave in place, and this field's value is the
organization name and ROR at the top of this section.

**Considered and rejected:** promoting the 85 contributors listed on the Zenodo record (Beggan and
Kloss as ProjectLeader, the remainder as Researcher/Other, each with an ORCID) or the 85 authors of
the IGRF-14 paper into this field. The release credits IAGA as its sole *creator* and lists those
individuals as *contributors*; the distinction is upstream's and is preserved. Their scientific credit
is carried by the reference publication in Field 14.

### 7. Software Name (MANDATORY)
IGRF-14

The title of the Zenodo release record, verbatim, and the form of the name used on the NCEI product
page. The expanded form ("International Geomagnetic Reference Field") opens the description rather
than displacing the short name, which is how the community refers to a specific generation.

### 8. Description (MANDATORY)

> The International Geomagnetic Reference Field (IGRF) is a standard mathematical description of the
> Earth's main magnetic field. It is used widely in studies of the Earth's deep interior, crust,
> ionosphere, and magnetosphere. The model is developed and maintained by the International
> Association of Geomagnetism and Aeronomy (IAGA). The coefficients for the 14th generation of IGRF
> model were finalized by an IAGA task force in November 2024. The IGRF is the product of a global
> collaborative effort between magnetic field modelers and the institutes involved in collecting and
> disseminating magnetic field data collected from satellites, observatories, and surveys around the
> world.
>
> This is the fourteenth generation of the model, IGRF-14, which covers the period from 1900 to 2030.
> It incorporates the Definitive Geomagnetic Reference Field (DGRF) for 2020.0, which supersedes the
> preliminary estimate for that epoch provided in IGRF-13.
>
> For more information, see
> https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field
>
> The model coefficients are provided in three formats:
> - igrf14coeffs.txt - traditional format compatible with previous IGRF releases
> - IGRF14coeffs.xlsx - Excel equivalent of the above
> - IGRF14.shc - SHC format compatible with ESA Swarm mission software (see description here:
>   https://spacecenter.dk/files/magnetic-models/CHAOS-5/SHC-Format-Decsription.pdf)
>
> NB: "Version v2" on the Zenodo record includes a fix to the format of the .shc file.
>
> You can cite the Zenodo record (i.e. the IGRF-14 coefficients themselves) as: International
> Association of Geomagnetism and Aeronomy. (2024). IGRF-14. Zenodo.
> https://doi.org/10.5281/zenodo.14012302
>
> When using IGRF-14, you should cite: Beggan et al. International geomagnetic reference field: the
> fourteenth generation. Earth Planets Space 78, 127 (2026).
> https://doi.org/10.1186/s40623-025-02360-0
>
> A list of journal articles can be found as a topical collection in "International Geomagnetic
> Reference Field - The Fourteenth Generation" in Earth, Planets and Space:
> https://link.springer.com/collections/jecafgcbaf

This is IAGA's own description of the release, carrying the wording of the current Zenodo record. **An
older snapshot of the same upstream text is in circulation, and it is superseded** — a future agent may
meet it and should not reinstate it. Two distinct kinds of difference separate the two, and both are
needed to account for the gap: upstream revised its own prose, and the flattening of upstream's HTML
into plain text differs.

**Upstream's own revisions** (record metadata last modified 2026-07-03). The value above follows
upstream in each of these; none of this wording was composed to fill a gap.

1. **The citation instruction — the substantive difference.** The older text ends:

   > There will be a journal article in topical collection "International Geomagnetic Reference Field -
   > The Fourteenth Generation" in Earth, Planets and Space  that should be cited once it is published.

   That article has since been published, and IAGA replaced the forward-looking sentence with an
   instruction to cite Beggan et al. (2026), Earth, Planets and Space 78, 127,
   `https://doi.org/10.1186/s40623-025-02360-0` — the same paper recorded in Field 14 — followed by a
   pointer to the topical collection.
2. **The `.shc` version note was reworded**, from `NB: "Version v2" on Zenodo includes a fix…` to
   `NB: "Version v2" on the Zenodo record includes a fix…`. The note itself is retained because it is
   real provenance for the v2 release, corroborated independently under Field 12.
3. **The Zenodo-citation sentence gained a parenthetical**, from `You can cite the Zenodo record as:…`
   to `You can cite the Zenodo record (i.e. the IGRF-14 coefficients themselves) as:…`, distinguishing
   the citation for the coefficients from the citation for the paper.

**The plain-text rendering of upstream's HTML.** These differences are presentational, arising from the
flattening rather than from the metadata:

- **Non-breaking spaces (U+00A0) are normalised to ordinary spaces.** Upstream carries them after
  "which" (in "which covers"), after "as:" and after "cite:".
- **The `<br>` separators in the three-format list are rendered as line breaks.** In the older
  snapshot they had been dropped outright, running the list onto a single line — `three formats:-
  igrf14coeffs.txt - traditional format … - IGRF14coeffs.xlsx …`. The item text itself is unchanged.
- **The `<br>` after "as:" and the one after "cite:" are rendered as a single space**, so each
  citation runs on from the words introducing it. This does not reproduce upstream's line break, and
  neither did the older snapshot: it collapsed the "as:" break with no space at all, giving
  "as:International". An agent diffing this value against upstream character by character should
  therefore expect those two breaks to differ, rather than read the difference as corruption.
- **Hyperlink targets are represented by appending the URL after upstream's own link text, with a
  colon introducing it.** Upstream's link text is not altered in either case, and the two cases have
  different histories, which is worth keeping straight:
  - `see description here: https://spacecenter.dk/files/magnetic-models/CHAOS-5/SHC-Format-Decsription.pdf`
    (the SHC format description) is a genuine **restoration** — the older snapshot carried the phrase
    "(see description here)" with its target dropped, leaving "here" pointing nowhere. Upstream's
    phrase really is "see description here".
  - `… in Earth, Planets and Space: https://link.springer.com/collections/jecafgcbaf` (the Springer
    topical collection) is **not** a restoration, and should not be read as one. No such link existed
    in the older snapshot to lose: that sentence is part of upstream's citation revision described
    above, which replaced an entirely different, unlinked sentence. Only its rendering follows the same
    convention, with the colon standing in place of upstream's sentence-final period.

  Note that the upstream SHC filename contains the misspelling "Decsription"; it is correct as
  published and must not be "fixed", or the link breaks.

### 9. Concise Description (OPTIONAL)
The International Geomagnetic Reference Field (IGRF) is a standard mathematical description of the
Earth's main magnetic field.

This is the opening sentence of IAGA's own description. It fits the 200-character limit and is an
accurate stand-alone preview, so no alternative wording is needed here.

### 10. Publication Date (RECOMMENDED)
2024-11-22

**`2024-11-25` is the wrong value for this field, and an easy one to arrive at — it must not be
reinstated.** The field is defined as the date of first
publication, "used for the initial version of the software." The concept DOI has two version
records, and the initial one is record 14012303, published **2024-11-22**. Record 14218973, published
2024-11-25, is the *second* version, and its date is already carried by Field 12 as the version
release date.

Storing 2024-11-25 here both misstated first publication and duplicated Field 12, discarding the
first-publication information entirely. With the correction the pair is informative: the release was
first published 2024-11-22, and the current version v2 followed on 2024-11-25.

The 2024-11-25 value is nonetheless easy to arrive at innocently, which is why this note exists: the
Zenodo concept DOI and its DataCite record both report an `Issued` date of 2024-11-25, because a
concept DOI inherits the latest version's metadata rather than the earliest. The initial version's own
record is the authority for this field.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Correct per the field's guidance: the DOI was obtained through Zenodo, and DataCite reports
`publisher: "Zenodo"`.

**Considered and rejected:** naming IAGA or NOAA/NCEI as publisher. IAGA is the *creator* (Field 6),
and NCEI hosts the landing page and mirrors the artifacts but did not publish the DOI. The NCEI page
says so itself: "While this web page is hosted at NOAA/NCEI, the model itself is developed and
maintained by the International Association of Geomagnetism and Aeronomy (IAGA)."

### 12. Version (RECOMMENDED)
- **Version Number:** `v2`
- **Version Date:** 2024-11-25
- **Version PID:** https://doi.org/10.5281/zenodo.14218973
- **Version Description:**

> Corrects the format of the IGRF14.shc coefficient file. The coefficient values themselves are
> unchanged from the initial release of 2024-11-22: igrf14coeffs.txt and IGRF14coeffs.xlsx are
> byte-identical between the two version records, and IGRF14.shc is the only file that differs.

**The version label is `v2`, and upstream contradicts itself about this; it should not be "corrected"
to `v3`.** The conflict is set out in full because the evidence decides it, and because an agent
meeting only the `v3` side of it would otherwise reverse the choice:

- **Zenodo, the publisher of record, says `v2`.** The record page for 14218973 renders
  "| Version v2" in its header, and the page's embedded record JSON contains `"version": "v2"`.
  The string `v3` does not appear anywhere in that page as retrieved.
- **Zenodo's own version index corroborates it.** The same embedded JSON reports
  `"versions": {"index": 2, "is_latest": true}`, and the concept DOI has two version records —
  14012303 and this one. This record is the second of the two, consistent with `v2` and inconsistent
  with `v3`.
- **IAGA's own description says `v2`**: `NB: "Version v2" on the Zenodo record includes a fix to the
  format of the .shc file.`
- **DataCite says `v3`**, for both `10.5281/zenodo.14218973` and the concept DOI. This is the source a
  `v3` label traces back to, since DOI-based autofill draws on DataCite. It is the outlier: it is
  contradicted by the publisher's rendering, the publisher's embedded metadata, the version index,
  and the creator's own prose.
- Zenodo's machine-readable metadata carries no version value at all for either record, so it neither
  supports nor refutes either label; its silence is not evidence of an absent version.

**`2025-10-22` is not a release date at all, and is the wrong value for this field.**
That timestamp is the metadata-edit time of the *earlier* record 14012303 (last modified
2025-10-22T08:39:24). Record 14218973 was published 2024-11-25. A future agent encountering
2025-10-22 in any older artifact should treat it as this misattribution rather than as a third release.

**The version description previously restated the Field 8 description**, which conveyed nothing
about what changed in this version. It is replaced with an actual changelog, verified against the
artifacts rather than merely restated from upstream's note: comparing the two version records file by
file, `igrf14coeffs.txt` (`md5:3606931c15c9234d9ba8e2e91b729cb0`) and `IGRF14coeffs.xlsx`
(`md5:dd71a0f748f047704997743475c3209d`) are identical across both, while `IGRF14.shc` changes from
`md5:497a5c69dab42b53282f1e25df797fad` in 14012303 to `md5:12ca20c847385c9114103f301b898949` in
14218973. Of the three published files, `IGRF14.shc` is the one that differs, exactly as IAGA's note
describes.

The Version PID is the version-specific DOI and was already correct; Field 2 holds the concept DOI.

### 13. Programming Language (RECOMMENDED)
Not found — the release contains no source code. Documented omission.

**This is the scope decision that also governs Fields 18 and 19. It is the most consequential
judgement in this file, so the full reasoning is here.**

The NCEI product page distributes, alongside the coefficients, three pieces of *synthesis software*:
a Fortran program (`igrf14.f`), a Python package (`pyIGRF14.zip`), and the Geomag 7.0 command-line
distribution for Windows and Linux. It is tempting to read those as this entry's implementation and
fill Field 13 with Fortran and Python. **They are separate software and are excluded from this
record.** The evidence:

- **They are not part of the release.** The Zenodo record that Field 2 identifies contains three
  files, all data. No code is published under this DOI.
- **They have different authors.** The release credits IAGA as sole creator. `igrf14.f` credits Susan
  Macmillan, William Brown and Ciaran Beggan of the British Geological Survey; `pyIGRF14` is authored
  by Ciaran Beggan and is derived in part from ChaosMagPy.
- **They have three mutually incompatible licences — this is decisive.** The Zenodo coefficient
  release is CC-BY-4.0. `pyIGRF14` ships an MIT licence (`Copyright (c) 2024 Ciaran Beggan`).
  Geomag 7.0 is public domain: the NCEI page's statement that "The software code is in the public
  domain and not licensed or under copyright" appears under the heading "Geomag 7.0 License and
  Copyright Information" and is scoped to that program. (`igrf14.f` carries no licence statement at
  all.) If the synthesis programs were in scope, this entry's single Licence field could not be
  correct for most of its content. Keeping them out is what makes Field 15 coherent.
- **They are versioned and maintained independently.** `pyIGRF14`'s bundled CITATION file still
  directs users to the IGRF-13 paper, while the release record was updated in 2026 to cite the
  IGRF-14 paper. They do not move together.

Because the release is data, no programming language exists to report. **`Other` was considered and
rejected**: it would assert an unnamed language, which is false, whereas Fields 20 and 21 have genuine
"no constraint" values that can be stated truthfully (see those fields for the asymmetry). A
documented omission is the accurate outcome.

pyIGRF14 (MIT, British Geological Survey) and Geomag 7.0 (public domain, NOAA/NCEI) are separately
identifiable software in their own right, each with its own authorship and licence, rather than
components of this release. They are not carried in Field 29 either; see that field for why.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1186/s40623-025-02360-0

Beggan, C. D., Kloss, C., et al. (2026). *International geomagnetic reference field: the fourteenth
generation.* Earth, Planets and Space **78**(1), article 127. Published 2026-06-29; 85 authors; first
author ORCID `https://orcid.org/0000-0002-2298-0578`. Verified against Crossref.

This is the canonical reference publication on two independent grounds: it is the release record's
`IsDescribedBy` target, and IAGA's own description instructs, "When using IGRF-14, you should cite:
Beggan et al. …". The field was previously empty because the paper did not yet exist when the record
was created.

Note the DOI's `s40623-025-` segment implies 2025 while the article was published 2026-06-29. That is
a Springer DOI-assignment artifact, not an error in this value; the DOI resolves to the 2026 article
and is the identifier upstream links to.

**Considered and rejected: the IGRF-13 paper, Alken et al. (2021), EPS 73, 49,
`10.1186/s40623-020-01288-x`.** A future agent may well be tempted by it, because the NCEI product
page's own "Citation" section still cites the *13th* generation on the IGRF-14 page, and `pyIGRF14`'s
CITATION file does the same. Both are upstream staleness. That paper describes the previous
generation and is not this release's reference publication.

### 15. License (RECOMMENDED)
- **License:** Creative Commons Attribution 4.0 International
- **License URI:** https://spdx.org/licenses/CC-BY-4.0.html

The licence is the Zenodo record's, corroborated on both sides: the record's licence is `cc-by-4.0`,
and DataCite reports rights "Creative Commons Attribution 4.0 International" with SPDX identifier
`cc-by-4.0`. The URI above is the SPDX page for that identifier.

**Scope caveat — do not change this on the strength of the NCEI page's public-domain sentence.** That
page states "The software code is in the public domain and not licensed or under copyright," which
reads at a glance like a contradiction. It is not: the sentence sits under the heading "Geomag 7.0
License and Copyright Information" and applies to that NCEI-hosted synthesis program, which is out of
scope for this record (Field 13). The Zenodo coefficient release this entry describes is CC-BY-4.0,
and a third licence again — MIT — governs `pyIGRF14`. Three licences coexist on that page because
three different things are being distributed.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- igrf
- igrf14
- geomagnetism
- geomagnetic field
- earth magnetic field
- magnetic field modeling
- empirical model
- main field
- secular variation
- spherical harmonics
- gauss coefficients
- dgrf
- core field
- crustal field
- declination
- inclination

**Negative research: there is no upstream keyword source for this release.** The Zenodo record carries
no keywords and DataCite's `subjects` is empty, and the release is absent from all three PyHC
registries (core, community and unevaluated), so no curated PyHC keyword set exists either. Their one
IGRF project entry, as of this extraction, is IGRF-13 (`space-physics/igrf`) — a third-party
Python/Matlab implementation of the model, not this release. Every keyword above is therefore derived
from the science content of the release, its coefficient files, and the NCEI product page, rather than
copied from a metadata field.

Each keyword was chosen for a specific reason:

- `igrf`, `igrf14` — the model and this generation of it, the first terms a user searches on. Both are
  needed: `igrf` reaches anyone looking for the model family, while `igrf14` distinguishes this
  generation from its predecessors, which matters for a model that is revised on a five-year cycle and
  whose generations are not interchangeable.
- `geomagnetism`, `geomagnetic field`, `earth magnetic field` — the field of study and the quantity
  modelled, in the phrasings the sources use interchangeably. All three are kept because they are not
  reliably substitutable in search.
- `magnetic field modeling`, `empirical model` — what the release is: a model of the field, fitted to
  observations rather than derived from governing equations (the same distinction Field 4 records).
- `main field`, `secular variation` — the two components the release actually contains. The coefficient
  header distinguishes "main-field models" (degree 13) from "secular variation" (degree 8, nT/year),
  and the predictive SV is what extends coverage to 2030.
- `spherical harmonics`, `gauss coefficients` — the mathematical representation and the literal content
  of the files ("Schmidt semi-normalised spherical harmonic coefficients"). The plural `spherical
  harmonics` is used in preference to the singular `spherical harmonic`. `gauss coefficients` is a term
  of art in geomagnetism for the coefficients of this expansion, and is unrelated to the similarly
  spelled statistical terminology of Gaussian processes.
- `dgrf` — the Definitive Geomagnetic Reference Field, named in the description and in the coefficient
  table's column headers. It is the distinction that explains why IGRF-14 supersedes IGRF-13's
  provisional 2020.0 estimate, and it is the term researchers search on.
- `core field`, `crustal field` — these carry the two application areas the Region vocabulary cannot
  express (see Field 5). The description names the Earth's "deep interior" and "crust" alongside the
  ionosphere and magnetosphere; without these keywords those two areas would vanish from the record
  entirely.
- `declination`, `inclination` — the field elements users most often compute from the coefficients, and
  the terms under which non-specialists look for the model.

**Deliberately excluded: `ionosphere` and `magnetosphere`.** The field is for science keywords "not
supported by other metadata fields," and both are already carried by Field 5. Duplicating them here
would add no discoverability.

### 17. Data Sources (OPTIONAL)
Not found. Documented omission.

The field records the data input sources *the software supports*. This release is a published
coefficient set: it retrieves nothing, queries no archive, and has no input path at all. Selecting any
source would describe software that does not exist here.

**Considered and rejected**, because both are genuinely tempting and neither survives the field's
definition:

- `WDC` — the NCEI page credits "World Data Centers" among the bodies whose data supported the IGRF
  project, and the coefficient files were built from satellite, observatory and survey measurements.
  But that describes how the model was *constructed*; it is not an input source this artifact reads.
- `VirES` — ESA's Swarm data service. The connection is only that the release ships an `.shc` file in
  a format Swarm tooling reads (see Fields 31–32), which is an output-format compatibility statement,
  not a data source the release consumes.

### 18. Input File Formats (RECOMMENDED)
Not found. Documented omission — see Field 13 for the governing scope decision.

The release performs no file input. The form is explicit that "Only formats actually supported should
be indicated," and support here means the software reads such files; a static data release reads
nothing.

### 19. Output File Formats (RECOMMENDED)
Not found. Documented omission — see Field 13 for the governing scope decision.

The field asks for formats the software "supports for generated files," which presupposes runtime
output. The release generates nothing; it *is* its files.

**The distribution formats are recorded here as provenance, and as a conditional path for whoever
revisits this.** The release is published as `igrf14coeffs.txt` (plain ASCII text), `IGRF14.shc`
(SHC, also a text format) and `IGRF14coeffs.xlsx` (Excel). If a future curator decides that
*distribution* format is what this field should capture for data releases, then `ascii` would be the
supportable value for the first two, and `Other` the sole remaining option for the third — this field
offers no `xlsx` or `shc` term. That reading was considered and not adopted,
because it conflicts with the form's "generated files" wording; the alternative is set out so the
choice can be made deliberately rather than rediscovered.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

The value is written out in full; the abbreviated "OS Independent" is not an accepted spelling of it.

The release's artifacts are platform-neutral text and spreadsheet files, usable on any operating
system. `Operating System Independent` asserts precisely that — the *absence* of a platform
constraint — which is a true and useful statement about this release, and it lets a user distinguish
"unconstrained" from "not yet filled in."

**Note the deliberate asymmetry with Field 13.** Field 13 is omitted while this field is populated,
and that is not an inconsistency: this field offers a value meaning "no constraint," which is true
here, whereas Field 13's only fallback (`Other`) would assert an unnamed language that does not exist.
Populated where the field can express "none", omitted where filling it would require inventing a
positive fact.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Same reasoning as Field 20: coefficient files in text and spreadsheet form impose no architecture
requirement, and `CPU Independent` states that truthfully rather than enumerating specific
architectures, none of which the release constrains.

### 22. Related Phenomena (OPTIONAL)
Not found. Documented omission.

**This field is a closed list, and none of its allowed values applies.** As of this extraction its
terms are `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`,
`Solar Flares`, `Solar Wind` and `X-ray emission` — solar and heliospheric phenomena, plus geomagnetic
storms. IGRF-14 describes the Earth's *internal* main field and its slow secular variation, for which
there is no allowed value, and this field does not admit free text. The phenomena-adjacent concepts are
carried instead by Field 16, where they are expressible.

**`Geomagnetic Storms` was considered and rejected.** The association is real but inverted: IGRF is
the quiet-time internal baseline that storm studies *subtract* in order to isolate the external
disturbance field. The model deliberately does not represent storm-time fields, and neither the
release description, the NCEI product page nor the IGRF-14 papers connect it to storms. Selecting it
would misrepresent what the model does.

### 23. Development Status (RECOMMENDED)
Active

The repostatus.org terms describe code repositories, which makes this an imperfect fit for a
coefficient release; `Active` is nevertheless the honest choice. IGRF-14 has reached a stable, usable,
published state and remains the current authoritative generation, maintained by the IAGA V-MOD working
group on a five-year revision cycle. Maintenance is demonstrable rather than assumed: the working
group issued a corrected v2 of the release, and revised the record's metadata in 2026 to add the
newly published reference publication.

**`Inactive` was considered and rejected.** Its definition — "no longer actively developed" — would
imply to users that IGRF-14 is superseded or unsupported, which is false while it remains the standard
in force. `Abandoned`, `Unsupported`, `Suspended`, `Moved`, `Concept` and `WIP` are all plainly
contradicted by a finalized, published, community-standard model.

### 24. Documentation (RECOMMENDED)
https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field

The NCEI product page is the model's documentation hub: it carries the mathematical specification
(the field as the negative gradient of a scalar potential expanded in spherical harmonics, with
reference radius a = 6371.2 km and truncation degree N = 13), the validity ranges, the table of all
prior generations, access to the coefficients and synthesis programs, and links to the online
calculators.

This deliberately repeats the Field 3 value, which the field's own guidance sanctions: "If this is the
same as the access URL, then enter that link here." The field was previously empty.

**Considered and rejected:**

- The IGRF Health Warning page
  (`https://www.ncei.noaa.gov/products/international-geomagnetic-reference-field/health-warning`) — a
  substantive document by F. J. Lowes of IAGA Working Group V-MOD on the model's errors and
  limitations, and genuinely valuable. Rejected as the primary documentation link because it is scoped
  to caveats rather than use, and because it is itself stale: revised January 2010 and still stating
  that the latest generation is the 13th. Recorded here so its existence is not lost.
- The Zenodo record page — it reproduces the description and hosts the files, but documents neither
  the model's mathematics nor its use.

### 25. Funder (OPTIONAL)
Not found. Documented omission.

**Negative research:** DataCite's `fundingReferences` for both the version and concept records is
empty. The NCEI product page thanks the participating institutes and "the many organizations involved
in operating magnetic survey satellites, observatories, magnetic survey programs and World Data
Centers" but names no funder.

The IGRF-14 papers do carry a Funding section, and it is worth being precise about what it contains,
because it looks at first glance like a source for this field and is not. What it credits is the
funders of the *contributing satellite missions and of the authors' research*. Its entries include the
European Space Agency, which owns and operates Swarm and CryoSat-2; the Danish government, NASA, ESA,
CNES, DARA and the Thomas B. Thriges Foundation for Ørsted; DLR for CHAMP (grant code 50EE0944); CONAE
with NASA/JPL and the Danish Space Research Institute for SAC-C; CNSA and CEA for CSES; CNSA and the
Macau Foundation for MSS-1; CNES for the French Swarm contribution; the European Research Council
(GRACEFUL Synergy Grant 855677); ESA again under EO Science for Society (contract
4000127193/19/NL/IA, "Swarm +4D Deep Earth: Core"); a NOAA cooperative agreement (NA22OAR4320151); and
budgetary funding of the Geophysical Center of RAS and the Schmidt Institute of Physics of the Earth of
RAS for the Russian contribution — alongside the institutes, staff and INTERMAGNET who support the
international observatory network.

What matters for this field is that every one of those funds an *input* to the model, or research
around it, rather than the production or publication of the coefficient release this record describes.
So the papers name funders, but not a funder of this software. That conclusion does not depend on the
list above being complete, and a reader should not treat it as an exhaustive transcription of the
section.

IGRF is a volunteer international working-group product; no funding body is credited for the release
itself.

### 26. Award Title (OPTIONAL)
Not found. Documented omission — no award or grant is identified anywhere in the release metadata or
on the NCEI product page, consistent with the absence of a funder in Field 25.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1186/s40623-026-02382-2

Beggan, C. D., Kloss, C., Grayver, A., Alken, P., et al. (2026). *Evaluation of candidate models for
the 14th generation International Geomagnetic Reference Field.* Earth, Planets and Space **78**(1),
article 126. Published 2026-06-29; 31 authors. Verified against Crossref.

Recorded on the authority of the release record's own `IsSupplementedBy` relation to this DOI. It is
the companion paper to the reference publication: it documents how the candidate models submitted by
the participating teams were evaluated to produce the adopted coefficients, which is exactly the
context a user of the coefficients needs. It is kept distinct from Field 14, which holds the paper
describing the model itself.

**Considered and rejected:**

- Alken et al. (2021), `10.1186/s40623-020-01288-x` — the IGRF-13 paper. It describes the previous
  generation, not this release. See Field 14 for why upstream pages nonetheless still cite it.
- The Earth, Planets and Space topical collection
  (`https://link.springer.com/collections/jecafgcbaf`) — a collection of many articles rather than a
  publication with its own DOI, so it does not fit this field's DOI-per-entry form. It is preserved in
  the Field 8 description instead, which is where upstream puts it.

### 28. Related Datasets (OPTIONAL)
Not found. Documented omission.

The field is for datasets the software supports functionality for. This release *is* the data product,
so the relation has no natural subject here. The satellite, observatory and survey measurements from
which the coefficients were derived would be the candidates, but neither the release metadata nor the
NCEI product page identifies any of them by DOI or persistent identifier, and inventing dataset
citations is not an option. The earlier version record under the same concept DOI is not a related
dataset — it is a prior version of this record, already accounted for in Fields 10 and 12.

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.14205633 — IGRF-14 Evaluation
- https://doi.org/10.5281/zenodo.5962660 — ppigrf (Pure Python IGRF)

**IGRF-14 Evaluation** is the software used to collate and evaluate the candidate models that
produced this release. It is recorded on the authority of the release record's own `IsSupplementedBy`
relation, with `resourceTypeGeneral: Software`; the eval record reciprocates with `isSupplementTo` the
release concept DOI, and is itself documented by the Field 27 evaluation paper. The concept DOI is
used in preference to the version DOI `10.5281/zenodo.14205635`, per this field's guidance to prefer
the software's DOI at the all-versions level. Of the related software, this is the entry that most
distinguishes the release: it is how the coefficients here came to be chosen.

**ppigrf** is the IAGA V-MOD working group's own pure-Python implementation for evaluating IGRF
generations — software performing a similar task, from the same body that maintains the model. The
specific evidence tying it to *this* release rather than to IGRF generally is its 2.0.0 release
(version DOI `10.5281/zenodo.14231854`, 2024-11-27), whose changelog reads "Default model changed
from IGRF-13 to IGRF-14" and lists "Add IGRF-14", "Updated IGRF14 SHC file" and "Add IGRF 14
reference". The concept DOI `10.5281/zenodo.5962660` is recorded so the entry tracks all versions;
the repository is `https://github.com/IAGA-VMOD/ppigrf` (MIT, actively maintained).

**Considered and rejected**, with reasons, so these are not re-proposed:

- **The NCEI-hosted synthesis programs** — `igrf14.f`, `pyIGRF14` and Geomag 7.0. They are out of
  scope as this entry's implementation (Field 13), and they also fail this field's practical
  requirement: no DOI or code repository was found for any of them, and their landing page is the
  NCEI product page already recorded as Field 3. An entry pointing back at this record's own Field 3
  URL would be circular and would tell a reader nothing. They are separately identifiable software,
  considered here and excluded from this release's related-software values.
- **Third-party IGRF implementations** — `space-physics/igrf`, `igrfpy`, Harmonica, ChaosMagPy and
  others. Each evaluates or repackages IGRF coefficients, but none was found to be tied to this
  release by an authoritative relation, and admitting them has no principled stopping point: IGRF has
  many independent implementations across several languages. The two entries above are included
  precisely because each has a documented relation to this release (one via the release's own
  metadata, one via its own changelog).
- **The World Magnetic Model** — genuinely the closest parallel product, a spherical-harmonic main
  field model with predictive secular variation, published by the same NCEI. Rejected because no
  authoritative relation connects it to this release; it is a parallel standard rather than a
  predecessor, companion or dependency, and admitting parallel standards would extend to every
  generation of WMM, and onward to CHAOS, POMME and EMM. Recorded here as the strongest discretionary
  candidate, so that a curator who judges the association worthwhile can add it as a deliberate choice
  rather than rediscovering the question.
- **The Zenodo archive of IGRF-13 coefficients**, concept DOI `10.5281/zenodo.11269409` (CC0). A
  future agent hunting for "the predecessor release" will find this and should not use it: it is a
  third-party archive by the Fatiando a Terra Project, created to serve as a data source for the
  Harmonica package, not an IAGA release. No IAGA-published Zenodo record for IGRF-13 was found —
  IAGA's Zenodo publication of the coefficients appears to begin with generation 14, which is
  consistent with only two version records existing under this concept DOI. The predecessor relation
  is instead expressed where the evidence actually supports it: in Field 8, which records that IGRF-14
  supersedes IGRF-13's preliminary 2020.0 estimate.

### 30. Interoperable Software (OPTIONAL)
Not found. Documented omission.

The field requires a demonstrated exchange with a named peer tool. For a published coefficient set,
that test degenerates: *any* IGRF-capable software "interoperates" with this release simply by reading
its files, so listing such tools would assert nothing specific about this record. The genuine
relationships that do exist are recorded in Field 29, where "performs a similar task" is the
applicable relation.

**The two near-misses, recorded so the reasoning is not repeated:**

- **"ESA Swarm mission software."** The release describes `IGRF14.shc` as "SHC format compatible with
  ESA Swarm mission software." This is a *format compatibility* statement about an unnamed family of
  tools, not a demonstrated exchange with an identified package, and there is no DOI or repository to
  record. It also does not make Swarm a related observatory — see Fields 31–32.
- **ChaosMagPy** (`10.5281/zenodo.3352398`), the tool most associated with the SHC format, whose
  format description this release links to. The documented link that was found runs through
  `pyIGRF14`, which is "partially based on ChaosMagPy" — and `pyIGRF14` is out of scope for this
  entry (Field 13). A relation mediated by out-of-scope software is not evidence of this release's own
  interoperability.
  Should direct evidence emerge that the release's `.shc` artifact is a documented ChaosMagPy
  interchange target, this is the entry to add.

### 31. Related Instruments (OPTIONAL)
Not found. Documented omission — no instrument is related, so nothing was carried to resolution.

**IGRF-14 is a global, instrument-agnostic empirical model, which means it supports no instrument
specifically.** It does not read, parse, calibrate or process any instrument's data; it is a set of
coefficients describing the whole Earth's main field. Applying the field's sanity check honestly: a
user searching for a specific instrument would not expect a global reference field model in the
results, and someone working with that instrument's data would reach for IGRF-14 only in the way they
would reach for any universal reference — not because it supports their instrument.

**The distinction that matters here, and the trap to avoid: the data that *fed* the model is not the
same as software *designed to support* that instrument.** The coefficients were derived from
measurements by magnetic survey satellites and ground observatories, and the NCEI page credits "the
many organizations involved in operating magnetic survey satellites, observatories, magnetic survey
programs and World Data Centers." Each of those contributing platforms looks like a candidate, and
none qualifies: their data was an input to the model's *construction*, whereas this field records
instruments the software is built to support. Neither the release metadata nor the NCEI page names a
specific instrument in any case.

This is a relevance decision rather than a failed lookup. No candidate was ever carried as far as
needing a SPASE identifier, because none is related in the first place: there is simply no related
instrument to record.

### 32. Related Observatories (OPTIONAL)
Not found. Documented omission — no observatory or mission is related, for the same reason as
Field 31.

**The Swarm question, answered explicitly because the record invites it.** The release description
says `IGRF14.shc` is in "SHC format compatible with ESA Swarm mission software." That is **mere
format compatibility, not designed-to-support evidence.** The release ships one of its three files in
a text format that the Swarm/CHAOS modelling community standardised, so that community's existing
tools can load it. It does not read Swarm data, implement Swarm data conventions as a means of
supporting the mission, process Swarm products, or model Swarm's measurements. Nothing about the
coefficients is Swarm-specific — the same file serves any tool that reads SHC. The Swarm mission's
measurements are among the many observations that contributed to the model's construction, which
Field 31 explains is the wrong basis for an association.

Recording ESA Swarm here would misrepresent a general-purpose model as mission-specific software, and
would return IGRF-14 to users searching for Swarm-supporting tools. The same reasoning excludes the
other platforms whose data historically supports IGRF, none of which the release metadata or the NCEI
page names individually.

As with Field 31, the decision is that nothing is related, so no candidate observatory is left
awaiting a SPASE identifier.

### 33. Logo (OPTIONAL)
Not found. Documented omission.

IGRF-14 has no logo of its own. **The candidate found, and why it was not used:** the NCEI product
page displays an image marked up as the IAGA logo, at
`https://www.ncei.noaa.gov/sites/default/files/2022-04/download.jpg` (a small JPEG, 272×185). It was
rejected on two grounds. First, it is the *developing organization's* logo, not the software's;
recording it would present IAGA's institutional mark as IGRF-14's identity. Second, the field asks for
an image "stored online in a permanent place," and this is a non-descriptive content-management upload
path (`download.jpg` inside a dated folder) with no stability guarantee.

The URL is recorded rather than merely discarded so that a curator who decides an organizational logo
is acceptable can adopt it as a deliberate choice, and so a future agent does not spend effort
rediscovering it.
