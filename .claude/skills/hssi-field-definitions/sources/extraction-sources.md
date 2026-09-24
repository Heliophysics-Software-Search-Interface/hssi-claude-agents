# Extraction sources — the autofill cascade and registries

<!-- Moved verbatim from resource_submission_form_fields.md lines 786-984 on 2026-09-22. Cross-field: each stage maps
     several fields to a source path. Field-specific consequences also appear in the relevant fields/NN file. -->

The HSSI web form supports automated metadata extraction through a cascade of API calls. AI agents can replicate this behavior to pre-fill many form fields automatically.

### Autofill Cascade Overview

The form uses a three-stage cascade when a DOI is provided:

1. **DataCite API** → Extract basic metadata from the DOI
2. **Zenodo API** (if applicable) → Get additional version and repository information
3. **SoMEF** → If a code repository URL was found, extract metadata directly from the repository

Each stage adds more metadata, with later stages filling in gaps or providing more detailed information.

---

### Stage 1: DataCite API

**Endpoint:** `https://api.datacite.org/dois/{DOI}`

**Example:** `https://api.datacite.org/dois/10.5281/zenodo.13287868`

**Fields Extracted:**
- **Software Name** (from `attributes.titles[].title`)
- **Description** (from `attributes.descriptions[]` where `descriptionType` may be "Abstract")
- **Concise Description** (from short descriptions ≤200 chars or truncated description)
- **Authors** with sub-fields:
  - Author name (from `attributes.creators[].name` or `givenName` + `familyName`)
  - Author Identifier (from `attributes.creators[].nameIdentifiers[]`): an **ORCID** (`nameIdentifierScheme` = "ORCID") for person creators, or a **ROR** (`nameIdentifierScheme` = "ROR", usually with `nameType` = "Organizational") for organization creators
  - Affiliations (from `attributes.creators[].affiliation[]`)
- **Publisher** (from `attributes.publisher`)
- **Publication Date** (from `attributes.dates[]` where `dateType` = "Issued")
- **License** name and URI (from `attributes.rightsList[]`)
- **Funders** (from `attributes.fundingReferences[].funderName`)
- **Awards** (from `attributes.fundingReferences[].awardTitle` and `awardNumber`)
- **Version Number** (from `attributes.version`)
- **Keywords** (from `attributes.subjects[].subject`)
- **Code Repository URL** (from `attributes.relatedIdentifiers[]` where `relationType` = "IsDerivedFrom" and `relatedIdentifierType` = "URL")
- **Documentation URL** (from `attributes.relatedIdentifiers[]` where `relationType` = "IsDocumentedBy")
- **Reference Publication** (from `attributes.relatedIdentifiers[]` where `relationType` = "IsDescribedBy")
- **Related Publications** (from `attributes.relatedIdentifiers[]` where `resourceTypeGeneral` is publication-related)
- **Related Datasets** (from `attributes.relatedIdentifiers[]` where `resourceTypeGeneral` = "Dataset")
- **Related Software** (from `attributes.relatedIdentifiers[]` where `resourceTypeGeneral` is software-related)

**How to replicate:**
```bash
# Example: Get metadata for a DOI
curl "https://api.datacite.org/dois/10.5281/zenodo.13287868"
```

---

### Stage 2: Zenodo API (Conditional)

**Endpoint:** `https://zenodo.org/api/records/{RECORD_ID}`

**When to use:** If the DOI is a Zenodo DOI (contains "zenodo" in the DOI)

**Example:** For DOI `10.5281/zenodo.13287868`, extract record ID `13287868` and query:
`https://zenodo.org/api/records/13287868`

**Additional Fields Extracted:**
- **Concept DOI** (from `conceptdoi`) - The DOI for all versions, not just one version
- **Version PID** (from `doi`) - The DOI for this specific version
- **Code Repository URL** (from `metadata.custom["code:codeRepository"]` - alternative source)
- **Development Status** (from `metadata.custom["code:developmentStatus"]`)
- **Programming Languages** (from `metadata.custom["code:programmingLanguage"][]`)

**How to replicate:**
```bash
# Extract Zenodo record ID from DOI
RECORD_ID=$(echo "10.5281/zenodo.13287868" | grep -oP 'zenodo\.\K\d+')

# Query Zenodo API
curl "https://zenodo.org/api/records/${RECORD_ID}"
```

---

### Stage 3: SoMEF (Conditional)

**When to use:** If a code repository URL was found in Stage 1 or Stage 2

**Tool:** [SoMEF](https://github.com/KnowledgeCaptureAndDiscovery/somef) (Software Metadata Extraction Framework)

**Installation:**
```bash
pip install somef
```

**Command:**
```bash
somef describe -t 0.7 -r {REPOSITORY_URL} -o output.json
```

**Fields Extracted:**
- **Persistent Identifier** (from `identifier[].result.value`)
- **Authors** with names and URLs (from `authors[].result`)
- **Software Name** (from `full_title[].result.value` or `name[].result.value`, choosing highest confidence)
- **Description** (from `description[].result.value`, may combine multiple with similar confidence)
- **Publication Date** (from `date_created[].result.value`)
- **Version Number** (from `version[].result.value`, choosing newest version)
- **Version Date** (from `date_updated[].result.value`)
- **Programming Languages** (from `programming_languages[].result.value`)
- **License** (from `license[].result` with `spdx_id` or `name`)
- **Keywords** (from `keywords[].result.value`, comma-separated)
- **Development Status** (from `repository_status[].result.description`)
- **Documentation URL** (from `documentation[].result.value`, prioritizing non-repository domains)
- **Logo** (from `logo[].result.value`)

**Notes:**
- SoMEF uses confidence scores; the implementation chooses results with highest confidence
- SoMEF can be slow (may take 30+ seconds for large repositories)
- The threshold `-t 0.7` means only results with ≥70% confidence are included
- Output format `-o` produces JSON-LD format

**How to replicate:**
```bash
# Example: Extract metadata from a GitHub repository
somef describe -t 0.7 -r https://github.com/SuperDARN/pydarn -o pydarn_metadata.json

# Read the output
cat pydarn_metadata.json
```

---

### PyHC Package Metadata

**What is PyHC?** The Python in Heliophysics Community (PyHC) maintains a registry of Python packages used in heliophysics research. If the software being submitted is a PyHC package, additional curated metadata may be available.

**PyHC Registry Files:**
PyHC maintains its package registry in three YAML files on GitHub. An AI agent should check all three to determine if the package is registered:

1. **Core packages:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_core.yml
2. **Community packages:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects.yml
3. **Unevaluated packages:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_unevaluated.yml

**Fields Available in PyHC Metadata:**
- **name** - Package name
- **description** - Package description
- **logo** - URL to package logo
- **docs** - Documentation URL
- **code** - Code repository URL
- **contact** - Primary contact/maintainer
- **keywords** - Array of keywords (may include domain-specific terms like "ionosphere_thermosphere_mesosphere", "magnetospheres", "solar", etc.)
- **community** - Quality rating for community engagement
- **documentation** - Quality rating for documentation
- **testing** - Quality rating for testing coverage
- **software_maturity** - Quality rating for software maturity
- **python3** - Quality rating for Python 3 compatibility
- **license** - Quality rating for license clarity

**How to check:**

1. **Read all three YAML files completely** - Don't use grep or search for specific terms, as you might use the wrong search term and miss a match
2. **Parse each file** and examine all entries to find matches based on:
   - Package name (may differ slightly from repository name)
   - Repository URL (code field)
   - Package description content
3. If found, extract the metadata from that entry
4. Use PyHC metadata to supplement other sources

**Example approach:**
```bash
# Download all three PyHC registry files for complete analysis
curl -s "https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_core.yml" -o pyhc_core.yml
curl -s "https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects.yml" -o pyhc_community.yml
curl -s "https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml" -o pyhc_unevaluated.yml

# Then parse each YAML file in its entirety to check for matches
# (Use a YAML parser to read all entries and compare against the package being analyzed)
```

**Important Notes:**
- Not all heliophysics packages are PyHC packages - absence from these files does not indicate a problem
- PyHC metadata is curated by the community and is considered more definitive/accurate than auto-extracted metadata
- The quality ratings (Good, Partially met, etc.) can inform the Development Status field
- PyHC keywords may map to HSSI's Related Region, Software Functionality, or Keywords fields
- **Its `logo:` value is an exception to that curation.** The registry's logo URLs are commonly
  branch-referenced (`.../main/...`) and sometimes point at a file that no longer exists. Treat the
  registry as authoritative about **which asset** is the project's logo, not about the URL string:
  re-derive the URL from the repository and pin it per the Field 33 guidance. Recording the registry's
  string verbatim is a defect even though the registry is otherwise the better source.

---

### Combining Results

The autofill cascade fills form fields in this recommended order:
1. **DataCite API** metadata is applied first
2. **Zenodo API** metadata overwrites/supplements DataCite data
3. **SoMEF** metadata is applied (only if repository URL was found)
4. **PyHC metadata** can supplement/replace any of the above, especially for logo, documentation, and keywords

Later stages generally don't overwrite fields that are already filled, unless the new data is more specific or complete. PyHC metadata, being manually curated, may be prioritized for certain fields like documentation URLs and description.

## General notes on extracting from a repository

<!-- Intro and closing sentences of the former RSFF "Notes for AI Agents"; the 16 numbered items moved to their fields. -->

When extracting metadata from a GitHub repository to fill this form:

Many fields are domain-specific (heliophysics) and may require understanding of the software's scientific purpose, which might be found in papers, documentation, or descriptive text in the README.

## Literature sources (when the repository is thin or absent)

<!-- moved from .claude/agents/hssi-metadata-extractor.md:190-226 -->
Some HSSI software has no source repository at all. A model or product page — a CCMC model page, a
mission software page — is then the authoritative source and a valid Field 3. Extract what is
discoverable and accept a thinner dossier; never invent a repository URL.

When the repo cannot supply a field, the literature usually can:

- **A publisher 402/403 is usually bot-blocking, not a paywall** — the article may be fully open
  access. Setting a browser User-Agent does *not* defeat it, and Unpaywall/Semantic Scholar often
  report an "open access" location that is the same blocked publisher URL. The portable route is
  **Europe PMC**: query
  `https://www.ebi.ac.uk/europepmc/webservices/rest/search?query=DOI:"<doi>"&resultType=core&format=json`,
  and if it returns `inEPMC=Y`, the corresponding PMC article page is readable by ordinary fetch,
  acknowledgements included. Coverage is partial — expect it to miss most AGU/Wiley papers.
  **If no route works, report it as a blocker in your result rather than recording the field as
  unavailable.** A browser renders these pages fine, and the orchestrator may have one; it can fetch
  the text and re-invoke you with it.
- **A paper's Acknowledgments and Data Availability Statement are the best source for Fields 25/26,**
  and are where code/data DOIs surface. See Field 25 in `hssi-field-definitions` for why they beat
  Crossref's funding block.
- **ADS/Sci-X needs no personal API token.** `GET https://scixplorer.org/v1/accounts/bootstrap`
  returns an anonymous token, usable as `Authorization: Bearer <token>` against
  `https://api.adsabs.harvard.edu/v1/search/query`. It supports `ack:` (acknowledgements section),
  `body:`, `full:`, proximity (`"a b"~N`) and fuzzy (`word~`). When the full text is unreachable,
  `ack:"<award>" bibcode:<paper>` still works as a membership probe — enough to settle which awards a
  paper acknowledges without reading it. Validate with controls: a nonsense token must return 0, and
  an award you believe absent should still be findable in *other* papers, proving real absence rather
  than a tokenization artifact. If the bootstrap stops working, it was a convenience route to
  full-text search — fall back to the routes above.
- **Semantic Scholar** (`api.semanticscholar.org/graph/v1`, no key) gives the citation graph, and its
  citation `contexts`/`intents` separate substantive use from a passing mention — which is what
  Fields 27 and 30 turn on. **OpenAlex** is open but its `grants` field is often null; don't rely on
  it for funders.

Searching the software's name alone misses artifacts that never name it. Award numbers, the PI's name,
or a companion dataset title are often better queries.

---

## Reaching blocked or tokenless sources (validator notes)

<!-- moved from .claude/agents/hssi-metadata-validator.md:171-173 -->
- A source returning 402/403 to an automated fetch is often bot-blocking, not genuine unavailability; the article may be fully open access. Try Europe PMC (`.../europepmc/webservices/rest/search?query=DOI:"<doi>"&resultType=core&format=json`; if `inEPMC=Y`, the PMC page is readable by ordinary fetch). A browser User-Agent does not defeat the block. If no route works, report the claim as **unverified for lack of access** rather than unsupported, and say which routes you tried — the orchestrator may have a browser and can supply the text
- **ADS/Sci-X needs no personal API token.** `GET https://scixplorer.org/v1/accounts/bootstrap` returns an anonymous token, usable as `Authorization: Bearer <token>` against `https://api.adsabs.harvard.edu/v1/search/query`. It supports `ack:` (acknowledgements section), `body:`, `full:`, proximity (`"a b"~N`) and fuzzy (`word~`). A report of "no ADS token available, claim unreproducible" is therefore a wrong premise, not a finding: run the bootstrap, re-check the claim, and validate with controls — a nonsense token must return 0, and a term you believe absent should still be findable in *other* records, so a real 0 is distinguishable from an auth failure. If the bootstrap stops working, fall back to the routes above.
