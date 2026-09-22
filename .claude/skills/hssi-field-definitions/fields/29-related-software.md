# Field 29 — Related Software

**Level:** OPTIONAL · **API:** `relatedSoftware[]` · **Change class:** enrich-only
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.4 (name) · **Field-search code:** `related`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 672-682; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — DOI URL preferred)

**What it is:** Software that performs similar tasks but does not necessarily link together (which would be 'interoperable software'). For example, two software that model the upper atmosphere of Earth but using different assumptions. Important software dependencies and software this work was forked from should also be included.

**When to include it (relevance):** List software that is *distinguishing* — it tells a reader something about **this** software. That means a package performing similar tasks, a predecessor or the project this was forked from, a companion package, or a **domain-specific** dependency (a heliophysics/science library whose presence characterizes the software). "Important software dependencies" means exactly that: *important*, not merely *present*. **The generic scientific-Python stack is excluded here too** — numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools and their peers are not related software, because listing them says nothing that isn't equally true of most of the ecosystem. Those names are **examples, not a closed list**: apply Field 30's "web app, finance model, or biology pipeline" test to anything unnamed, and treat generic infrastructure as excluded here too. Same test as Field 30: **if the entry would be equally true of most Python packages, it carries no information and does not belong.** The two gates are one rule — a package rejected from Field 30 is *not* thereby a Field 29 entry; it usually belongs in neither.

**How to fill it:** Ideally, enter the DOI for the software code. Otherwise, link to code repository (e.g., https://github.com/sunpy/sunpy). If no public repository, enter link where users can find more information (e.g., related HSSI item). Publication DOIs should go in relatedPublications instead.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

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
- Migrated from RSFF 672-682 on 2026-09-22.
