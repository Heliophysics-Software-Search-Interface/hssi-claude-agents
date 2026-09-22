# Field 30 — Interoperable Software

**Level:** OPTIONAL · **API:** `interoperableSoftware[]` · **Change class:** enrich-only
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.4 (name) · **Field-search code:** `interoperable`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 683-703; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — DOI URL preferred)

**What it is:** Other important software packages this software has demonstrated interoperability with. Can run package in the same environment as the others without errors.

**When to include it (relevance):** This field is about which other **high-level heliophysics/science tools** this software can actually interoperate with — **not its dependency list**. The bar is a *demonstrated exchange*: the two packages share or convert between data models, one's output can be imported into the other, there is an adapter/converter API (`to_sunpy_map()`, `from_pysat()`, `to_dataframe()`), a plugin/extension relationship, a companion package designed to be used with it, or a cross-language bridge to a named domain tool (an IDL SPEDAS or MATLAB interface). Read "can run in the same environment without errors" as presupposing that the two are **peer tools a user would deliberately combine** — it is a caveat on real interoperability, *not* the test for it. Merely sharing a Python runtime satisfies nothing.

**Never list these (Tier A), no exceptions:** numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools, and the rest of the generic scientific-Python/tooling stack. **Being a dependency is not interoperability.** "It directly depends on numpy" is true of nearly every package in HSSI, so it distinguishes nothing. General test: **if the claim would be equally true of most of the Python ecosystem, it carries no information about this software and does not belong here.**

**Tier A is a list of examples, not a closed list — the principle governs, not the names.** Do not conclude that a package is acceptable merely because it is not enumerated above. For any package not named in either tier, ask: **would this package be equally at home in a web app, a finance model, or a biology pipeline?** If yes, it is **generic infrastructure** — arrays, dataframes, plotting and mapping, I/O plumbing, packaging, testing, HTTP, logging, CLI parsing — and gets Tier A treatment whether or not it appears in the list. A genuine heliophysics/science peer tool fails that test immediately (it would be absurd in a finance model), so this rule does not put real domain software at risk.

**Include only with cited evidence (Tier B):** astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter and similar foundational-but-domain-adjacent packages. These qualify **only** when a specific exchange is documented in the public API, docs, examples, or tests — never on dependency presence alone. "The public API returns `xarray.Dataset` objects as its documented interchange format" qualifies; "uses xarray internally" does not. Two justifications that are **never** sufficient on their own: *"part of the standard scientific Python ecosystem"* and *"a PyHC member, so it interoperates with PyHC packages"* — ecosystem membership is not a demonstrated interoperation with any particular package.

**Worked contrast:** PySPEDAS ↔ PyTplot (exchanges tplot variables) ✅ · hapiclient ↔ hapiplot (companion visualization package) ✅ · sunpy ↔ ndcube (shared NDCube data model) ✅ · "depends on numpy" ❌ · "uses matplotlib for all plotting" ❌ · "listed in pyproject.toml dependencies" ❌.

**Where a rejected entry goes:** usually **nowhere**. A genuinely distinguishing domain package may belong in Field 29 (Related Software) — but Field 29 applies the same exclusion to the generic stack, so do not relocate a Tier A package there.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI page). Publication DOIs should go in relatedPublications instead.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:290-296 -->
**Related Software / Interoperable Software (Fields 29 & 30) — relevance gate.** Decide whether a package belongs at all **before** hunting for its DOI or repo URL. **Field 30 is about which other high-level heliophysics/science tools this software can genuinely interoperate with — it is not the dependency list.** The bar is a demonstrated exchange: a shared or converted data model, output from one imported into the other, an adapter/converter API (`to_sunpy_map()`, `from_pysat()`), a plugin/extension relationship, a companion package, or a cross-language bridge to a named domain tool (IDL SPEDAS, a MATLAB interface). Field 29 is for *distinguishing* software — similar-purpose tools, a predecessor or fork parent, a companion, or a domain-specific dependency. Specifically **exclude from both fields** (and record a brief `Note:` for anything you considered and dropped, so there's an audit trail):
- **Tier A, always** — numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools and the rest of the generic scientific-Python/tooling stack. Being a dependency is not interoperability; "it directly depends on numpy" is true of nearly every package in HSSI. **These are examples, not a closed list** — for any package not named in either tier, ask *would it be equally at home in a web app, a finance model, or a biology pipeline?* If yes it is generic infrastructure (arrays, dataframes, plotting/mapping, I/O plumbing, packaging, testing, HTTP) and gets Tier A treatment regardless. Never conclude a package is acceptable just because it isn't enumerated;
- **Tier B without cited evidence** — astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter qualify only when a *specific* exchange appears in the public API, docs, examples, or tests. "Public API returns `xarray.Dataset` as its documented interchange format" passes; "uses xarray internally" does not;
- **blanket ecosystem claims** — "part of the standard scientific Python ecosystem" and "a PyHC member, so it interoperates with PyHC packages" are never sufficient by themselves;
- **anything true of most Python packages** — if the entry would read the same for an arbitrary package, it carries no information and does not belong.

A package bumped out of Field 30 does **not** automatically land in Field 29 — the same Tier A exclusion applies there, and the usual correct destination is neither. For each package that *does* pass, record a DOI or repo URL as the form text requires, and make the source note name the **specific evidence** (the adapter function, the doc page, the example, the test) rather than "dependencies."

<!-- moved from .claude/agents/hssi-metadata-validator.md:158-166 -->
**Fields 29 & 30 (Related / Interoperable Software):**
- **Field 30 is not a dependency list.** It records other high-level heliophysics/science tools this software genuinely interoperates with — a shared or converted data model, output from one imported into the other, an adapter/converter API, a plugin/companion relationship, or a cross-language bridge to a named domain tool. Field 29 records *distinguishing* software (similar-purpose tools, predecessor/fork parent, companion, domain-specific dependency).
- **Over-inclusion.** For each listed entry, demand the specific exchange evidence — a named function, doc page, example, or test.
  - A **Tier A** package under either field (numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools and the rest of the generic stack) is an **ERROR**, with `Suggested fix: remove — a dependency shared by most of the Python ecosystem is not interoperability`. No evidence rehabilitates a Tier A entry.
  - **Tier A is examples, not a closed list — do not pass an entry merely because it isn't named.** For any package absent from both tiers, apply the test: *would it be equally at home in a web app, a finance model, or a biology pipeline?* If yes, it is generic infrastructure (arrays, dataframes, plotting/mapping, I/O plumbing, packaging, testing, HTTP) and takes the Tier A **ERROR** treatment. A real heliophysics/science peer tool fails that test immediately, so this does not endanger genuine domain entries.
  - A **Tier B** package (astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter) with no cited exchange is a **WARNING**. A cited, specific exchange ("public API returns `xarray.Dataset` as its documented interchange format") is acceptable; "uses xarray internally" is not.
  - Reject these justifications by name wherever they appear in a source note: *"listed as a dependency"* / *"in pyproject.toml"*, *"part of the standard scientific Python ecosystem"*, and *"PyHC member, so it interoperates with PyHC packages."* Ecosystem membership is not interoperation with any particular package.
  - The fix is normally **removal, not relocation to Field 29** — Field 29 applies the same Tier A exclusion.
- **Under-inclusion.** Check README, docs, examples, and tests for genuine interoperability with named domain tools that is *missing* from Field 30 — `to_*`/`from_*` converters, documented export→import handoffs, companion or plugin packages, shared data models. Flag these as WARNING/SUGGESTION. The gate is not purely subtractive: a real interoperability partner left out is as wrong as numpy left in.

<!-- moved from .claude/agents/hssi-metadata-updater.md:182-182 -->
**Relevance gate (Fields 29 & 30):** likewise apply the **`hssi-metadata-extractor`'s Fields 29/30 relevance gate** to any Related/Interoperable Software this extraction produces. Never enrich a Tier A generic dependency (numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, … — examples, not a closed list; anything equally at home in a web app, a finance model, or a biology pipeline is generic infrastructure and gets the same treatment) into either field, and enrich a Tier B package (astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter) only on cited evidence of a specific exchange. Field 30 is not a dependency list, and a package rejected from 30 is not thereby a Field 29 entry. Since both fields are enrich-only, this mode is the main path by which a generic dependency would otherwise reach a live HSSI entry.

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- phase2 -->

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 683-703 on 2026-09-22.
