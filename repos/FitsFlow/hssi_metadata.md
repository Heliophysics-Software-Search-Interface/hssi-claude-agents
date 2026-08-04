# HSSI Metadata Extraction Results

**HSSI Software ID:** 8054183f-794a-4914-a8cb-a379bb9f1040
**Repository:** https://github.com/indiajacksonphd/FitsFlow
**Source Revision:** 6111c361d58f4ccd60b0ee49b0da6165ab01a78b
**Extraction Date:** 2026-08-03
**Validation Date:** 2026-08-04
**Validation Status:** PASS

**Scope note.** FitsFlow is a deployed cloud service, not an installable library. The repository
contains the client (HTML/CSS/JavaScript) and the server-side AWS Lambda handlers, IAM policy
documents, and API/EventBridge definitions, but the running system lives at `https://www.fitsflow.org`
with its S3 bucket names and Lambda function ARNs redacted in-repo as `<BUCKET_NAME>`,
`<MAIN_FUNCTION>`, `<ASDF_FUNCTION>`. Functional evidence below is therefore drawn from the Lambda
source in `server/lambda_functions/` and the browser code in `client/`, which together describe the
complete pipeline even though the repository cannot be run as-is. There is no `CITATION.cff`,
`codemeta.json`, `.zenodo.json`, `AUTHORS`, `CONTRIBUTORS`, `setup.py`, `pyproject.toml`,
`package.json`, `requirements.txt`, `docs/` directory, or CI configuration in the repository; every
absence noted in the field entries below reflects that.

**Version currency.** The only git tag and the only GitHub release is `v.0.1.0`, and the 16 commits
between that tag and the pinned revision touch documentation and image assets only. See Field 12.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder is the settled state of this field, not an outstanding task. HSSI does not publish
the submitter of an existing record, and the submitter is not recoverable from the repository — no
file identifies who registered the entry — so there is nothing authoritative to substitute. A
placeholder is therefore the correct content here, and a future refresh should leave it rather than
guess.

It must not be filled with the author's identity: the submitter is whoever registered the metadata,
which is not necessarily the software's author. For correspondence, and *not* as a value for this
field, the author's contact address is `ijackson1@gsu.edu` (`client/html/index.html`, and the sole
git committer identity).

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.17069413`

Carried over from the existing HSSI record and confirmed to be the correct **concept** DOI, which is
what this field asks for. DataCite's record for `10.5281/zenodo.17069413` carries
`relatedIdentifiers: [{"relationType": "HasVersion", "relatedIdentifier": "10.5281/zenodo.17069414"}]`,
so 17069413 is the all-versions concept DOI and 17069414 is the version DOI — the latter belongs in
Field 12 (Version PID), where it is already correctly stored. The same DOI appears as the README's
Zenodo badge target and as the `DOI` element of the author's own SPASE record
(`spase://NSF/Software/FitsFlow`).

Considered and rejected: `https://doi.org/10.5281/zenodo.17069414`. That is the v.0.1.0 version DOI.
Because FitsFlow currently has exactly one release, the two DOIs describe the same content today,
which makes them easy to confuse — but the concept DOI is the stable choice and must not be replaced
by the version DOI when a second release appears.

### 3. Code Repository (MANDATORY)
`https://github.com/indiajacksonphd/FitsFlow`

Carried over from the existing HSSI record; matches the local clone's `origin` remote and the GitHub
API's `full_name` (`indiajacksonphd/FitsFlow`). The repository is public, not archived, not a fork,
default branch `main`.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: Movies
- Data Visualization: Web-Based
- Mission-related
- Mission-related: Science Data Processing
- Servers and Environments
- Servers and Environments: Data servers processing and handling
- Servers and Environments: Distribution/Access
- Servers and Environments: Infrastructure as Code
- Servers and Environments: Software or Environment Container

Every value above is an exact controlled-vocabulary term, written in the canonical `Parent: Child`
form.

All four top-level categories appear in their own right alongside their children, because **HSSI does
not infer a parent from a selected subcategory** — recording `Data Visualization: Movies` does not put
`Data Visualization` on the entry. Children without their parents is the standing failure mode for
this field, and it is why `Data Processing and Analysis`, `Data Visualization`, `Mission-related`, and
`Servers and Environments` are each listed.

Evidence for each value:

- **Data Processing and Analysis: Data Access and Retrieval** — FitsFlow retrieves from four remote
  services. `get_closest_image_id()` and `download_and_save_helioviewer_image()` call
  `api.helioviewer.org/v2/getClosestImage/` and `/v2/downloadImage/`; `fetch_hek_events()` calls
  `api.helioviewer.org/v2/events/` with `sources=HEK` over a 15-minute window from the observation
  time; `get_closest_jsoc_url()` walks JSOC's HTTPS directory index at
  `jsoc1.stanford.edu/data/{aia,hmi}/images/...`; `daily_videos.build_url()` fetches
  `sdo.gsfc.nasa.gov/assets/img/dailymov/...`. (All in `server/lambda_functions/`.)
- **Data Processing and Analysis: File Format Conversion** — the pipeline's central act. A FITS HDU
  becomes a NumPy `.npy` (`np.save`), a `.csv` (`pd.DataFrame(data).to_csv`), and a plain-text header
  dump (`upload_header_and_data()`); the JSOC JPEG 2000 / JPEG browse image is decoded and re-encoded
  as PNG (`download_jsoc_jp2()` → `Image.open(...)`, `img.save(png_buffer, format="PNG")`); and
  `lambda_asdf_function.py` assembles header text, HEK JSON, and file references into an ASDF tree
  written with `asdf.AsdfFile(tree).write_to(buffer, all_array_compression="zlib")`.
- **Data Processing and Analysis: Image Processing** — FITS pixel arrays are extracted from the
  correct HDU (`hdul[1] if len(hdul) > 1 and hdul[1].data is not None else hdul[0]`) and emitted as
  arrays; solar browse imagery is decoded and re-encoded through Pillow.
- **Data Processing and Analysis: Processing** — the multi-stage transformation chain in
  `process_fits_info()`: `hdul.verify('fix')` repair of nonconforming headers, `TELESCOP` gating,
  observation-time normalization across `T_OBS` / `DATE-OBS` / `DATE-OBS`+`TIME-OBS` including
  stripping the `_TAI` suffix, `dateutil` parsing, `WAVELNTH`→Helioviewer-source-ID and
  HMI `CONTENT`→`Ic`/`M` mapping, `Undefined`-card coercion when building `header_dict`, nearest-in-time
  file selection, and per-file skip accounting.
- **Data Visualization: Movies** — `daily_videos.py` downloads eleven SDO daily movies (AIA 0094,
  0131, 0171, 0193, 0211, 0304, 0335, 1600, 1700 plus `HMIIC` and `HMIB`) and concatenates them with
  `ffmpeg -f concat -safe 0 -i file_list.txt -c copy` into `{date}_stitched.mp4`, uploaded to
  `daily_videos/` in S3 on a nightly EventBridge schedule; `loadStitchedSDOVideo()` in
  `client/js/fitsFlow.js` renders that MP4 in the browser. The client additionally animates the
  processed image sequence (`togglePlay()` → `setInterval(nextImage, 300)`).
- **Data Visualization: Web-Based** — the entire user interface is browser-native: image carousel with
  prev/play/next, colour/grey tabs, a live pseudo-terminal log fed by `pollSingleLog()`, and an
  interactive collapsible HEK metadata tree (`new JSONFormatter(value, 0, { theme: 'dark' })`).
- **Mission-related: Science Data Processing** — retained from the existing record and independently
  supportable: FitsFlow processes exactly one mission's science data and rejects everything else
  (`if "SDO" not in tele.upper(): ... continue`, and `Skipping: {fname} — Unsupported instrument`
  for anything that is not AIA or HMI). This is the one value in the set whose parent category is a
  judgement call, and the tension is recorded on purpose rather than resolved away. The HSSI taxonomy
  reserves `Mission-related` primarily for mission ground-system software, and FitsFlow is a
  third-party tool rather than part of the SDO ground system, so that ground-system-versus-third-party
  test cuts against the value. The value is nonetheless the right one to keep, on exactly those
  grounds: it is a carried-over submitted value, it is defensible for a single-mission pipeline that
  handles no other mission's data, and no authoritative evidence shows it to be *wrong* — the
  objection is an argument about how to read the taxonomy, not a factual correction. A future refresh
  may revisit it if fresh evidence appears; until then the value stands, and this judgement is
  deliberately not extended to further `Mission-related` children (see the rejections below).
- **Servers and Environments: Data servers processing and handling** — the backend *is* an
  on-demand data-processing server: `server/apis/README.md` documents the `FitsFlow-2-Trigger-API`
  HTTP API Gateway endpoint, and `lambda_trigger_function.py` serves two modes behind it — mint a
  short-lived presigned S3 `put_object` URL (`ExpiresIn=300`), or asynchronously invoke the main
  processing Lambda.
- **Servers and Environments: Distribution/Access** — a documented delivery layer distinct from the
  compute API: CloudFront with Origin Access Control in front of a private S3 bucket, Route 53 DNS
  from `fitsflow.org` to the distribution (`server/README.md`), public-but-temporary output URLs of
  the form `https://www.fitsflow.org/temp/{session}/processed/...` valid for 24 hours, and
  client-side bulk bundling in `createZipFromPlaylist()` which fetches every product and emits
  `FitsFlow_Download_{date}_{time}.zip` with a generated `README.txt` manifest.
- **Servers and Environments: Infrastructure as Code** — retained and supported by
  `server/iam_policies/` (six files of declarative JSON: Lambda Trigger, Main, ASDF, Clean, the S3
  bucket policy and CORS configuration, and API Gateway) plus `server/apis/README.md`'s EventBridge
  rule `cron(0 4 * * ? *)`. Nuance for a future maintainer: these are JSON policy documents embedded
  in Markdown rather than a Terraform/CloudFormation/CDK template, so the repository declares its
  infrastructure without providing an executable deployment. The declaration is what this value
  claims; an executable deployment is not required for it.
- **Servers and Environments: Software or Environment Container** — retained.
  `server/lambda_layers/layer_urls.md` documents four prebuilt dependency layers (AWS SDK for Pandas
  via `arn:aws:lambda:us-east-1:336392948345:layer:AWSSDKPandas-Python310:25`, plus main, ASDF, and
  daily-videos `python.zip` bundles) "built on Amazon Linux EC2 to ensure binary compatibility with
  the AWS Lambda runtime (Amazon Linux 2)" and attachable as Lambda Layers. This value carries the
  same kind of tension as `Mission-related: Science Data Processing`, and it is kept for the same
  reason. The artifacts are **AWS Lambda Layers — packaged runtime environments, not OCI/Docker or
  Singularity containers**, and there is no `Dockerfile` anywhere in the repository, so a strict
  reading of "container" would exclude the value. It is kept because it is a carried-over submitted
  value that the packaged-runtime-environment reading supports, and no authoritative evidence shows
  it to be wrong. The objection is documented here so a future refresh finds it already weighed
  rather than re-deriving it.

Considered and **not** selected, with reasons — recorded so these are not re-proposed:

- **Data Visualization: 2D Graphics.** FitsFlow renders nothing. It displays PNGs that were rendered
  elsewhere (colourized by Helioviewer, greyscale browse products from JSOC) and emits its own FITS
  pixel data as CSV/NPY arrays rather than as a plot. There is no matplotlib, no plotting library, no
  canvas drawing code anywhere in the repository.
- **Data Processing and Analysis: ML/AI.** The description, the README, and the funding award all
  frame FitsFlow as producing *machine-learning-ready* outputs. It performs no machine learning: no
  model, no training, no inference, and no ML dependency appears in any Lambda or in the layer
  manifest. The distinction matters, because the NSF award abstract does describe AI/ML work — that
  work is the award's, not this release's.
- **Data Processing and Analysis: Time Series Analysis.** Nearest-in-time matching
  (`min(filenames, key=lambda f: abs((extract_dt(f) - target_dt).total_seconds()))`) and a 15-minute
  HEK event window are timestamp alignment, not analysis of time-ordered data.
- **Data Processing and Analysis: Analysis** and **Data Reduction.** No derived physical quantity is
  computed and no averaging, binning, or downsampling occurs; pixel data is passed through unchanged.
- **Data Processing and Analysis: Calibration.** FitsFlow consumes already-calibrated Level 1 SDO
  products (the bundle's generated `README.txt` says "derived from NASA SDO Level 1 FITS files") and
  applies no calibration of its own.
- **Coordinate Transforms** (any child). No coordinate system conversion occurs. Header keywords are
  read as strings and numbers; the WCS is never used.
- **Models and Simulations** (any child). Nothing is modelled or simulated.
- **Mission-related: Ingest.** The presigned-upload → S3 → Lambda-download path is a genuine ingest
  chain, but it ingests files a user chooses to upload rather than a mission's telemetry or data
  products, and `Mission-related: Science Data Processing` already carries the single-mission role.
- **Mission-related: Orchestration.** The trigger→main→ASDF Lambda invocation chain and the nightly
  EventBridge rule are internal cloud orchestration of FitsFlow's own compute, not mission
  operations orchestration; already conveyed by the `Servers and Environments` values.
- **Mission-related: Archive.** Outputs are deliberately ephemeral — `clean_s3_temp()` deletes
  everything under `temp/` nightly and the manifest warns that "access expires at midnight Eastern
  Standard Time." An archive is the opposite of the design.
- **Servers and Environments: High Performance Computing.** Lambda plus an optional, explicitly
  inactive EC2 worker ("Not currently active in production", `server/README.md`) is not HPC; there is
  no MPI, no scheduler, no parallel framework.

### 5. Related Region (MANDATORY)
- Chromosphere
- Corona
- Photosphere
- Solar Environment

All four are exact controlled-vocabulary terms; the Region vocabulary is flat, with no
`Parent: Child` form. `Solar Environment` comes from the existing HSSI record, and the three
finer-grained regions accompany it because the vocabulary supports that specificity and FitsFlow's
supported channel set names its regions explicitly.

The channel table in `client/html/index.html` and the source map in
`server/lambda_functions/helioviewer_source_id.json` together fix the regions:

- **Corona** — AIA 94 ("Hot flaring regions (~6.3 MK)"), 131 ("Flares & hot plasma"), 171 ("Quiet
  corona, loops (~0.6 MK)"), 193 ("Corona & flaring regions"), 211 ("Active regions (~2 MK)"), 335
  ("Hot active regions (~2.5 MK)").
- **Chromosphere** — AIA 304 ("Chromosphere & prominences"), and the example dataset shipped at
  `fitsflow.org/examples/05-01-2013-304/0304.zip` is "a dramatic prominence eruption captured in AIA
  304."
- **Photosphere** — AIA 1700 ("Photosphere"), AIA 4500 (`AIA_4500`, source_id 17, visible continuum),
  HMI Continuum ("Photospheric intensity (sunspot structure)"), and HMI Magnetogram ("Line-of-sight
  photospheric magnetism").
- **Solar Environment** — retained as the encompassing domain value for a tool whose whole purpose is
  solar imagery.

Considered and **not** selected:

- **Solar Interior.** The app's "Spacecraft" overlay explains that HMI is used to study "the Sun's
  internal structure through helioseismology." That describes the instrument's purpose, not
  FitsFlow's function: FitsFlow extracts single-image continuum and magnetogram products and performs
  no helioseismic inversion, so it supports no science functionality for the solar interior.
- **Earth Thermosphere / Earth Ionosphere / Earth Magnetosphere.** The description's closing sentence
  about "cyberinfrastructure that connects solar surface activity to radiation impacts in low Earth
  orbit (LEO)" is a statement of intent about future work in the wider award, not a capability of
  this software. Nothing in the code touches a terrestrial region.
- **Solar Wind** and **Interplanetary Space.** No in-situ or heliospheric data is handled.

### 6. Authors (MANDATORY)
1. **India Jackson**
   - Author Identifier: `https://orcid.org/0009-0001-5404-8689`
   - Affiliation: Georgia State University — `https://ror.org/03qt6ba18`

A single author, unchanged from the existing HSSI record, and confirmed to be complete by every
independent source: the sole git committer identity across all 132 commits is
`India Jackson, PhD <ijackson1@gsu.edu>`; DataCite lists one creator; the SPASE record lists one
author and one contact (`spase://SMWG/Person/India.Jackson`, roles PrincipalInvestigator, Developer,
TechnicalContact); and `client/html/index.html` credits "India Jackson, Phd" with the same ORCID.
No `CITATION.cff`, `codemeta.json`, `AUTHORS`, or `CONTRIBUTORS` file exists, so there is no other
author list to reconcile against. Nobody is dropped and nobody is added.

The stored name form is preferred over the alternatives on record. DataCite's creator block is
`{"name": "India Jackson, PhD", "familyName": "India Jackson, PhD", "nameIdentifiers": []}` — the
whole string was deposited as the family name and no ORCID was attached. HSSI's split into
givenName `India` / familyName `Jackson` with the ORCID is strictly better structured, so it stands.

The affiliation is confirmed authoritative rather than merely inherited: the ORCID record's current
employment is Georgia State University, department "Physics & Astronomy", role "Atmospheric &
Geospace Postdoctoral Fellow", 2025-02 to 2027-01, with ROR disambiguation
`https://ror.org/03qt6ba18` — the same ROR already stored — and that interval matches the NSF award
period (2025-02-15 to 2027-01-31). ROR resolves `03qt6ba18` to display name "Georgia State
University" (acronym GSU, Atlanta), so the stored organization name is the complete non-acronym form
Field 6 asks for. DataCite independently gives the creator's affiliation as "Georgia State
University".

Considered and **not** added as a second affiliation: "Georgia State University's Solar Informatics
and Data Mining Lab", named in the SPASE record's Acknowledgement ("FitsFlow was supported by
Georgia State University's Solar Informatics and Data Mining Lab"). That sentence acknowledges
support, and the author's ORCID employment names the department as "Physics & Astronomy" rather than
the lab, so an acknowledgement is not sufficient evidence for an affiliation claim. Also considered
and rejected: Frontier Development Lab and the National Aeronautics and Space Administration, both
present in the ORCID employment history but ended in 2024 and 2023 respectively, well before this
software existed (repository created 2025-08-25).

### 7. Software Name (MANDATORY)
FitsFlow

Carried over from the existing HSSI record and confirmed as the repository-listed name Field 7 asks
for: the GitHub repository is named `FitsFlow` and the README's first heading is `FitsFlow`.

Considered and rejected:

- **"FitsFlow: A Browser-Based Heliophysics Tool for FITS Exploration"** — the DataCite/Zenodo title.
  It is a descriptive title for the deposit, not the package name.
- **"FitsFlow v0.1.0"** — the SPASE `ResourceName`. Version-qualified; the version belongs in
  Field 12.
- **"FITSFlow"** — the casing used in the web app's `<title>` and navbar. It is a UI inconsistency,
  contradicted by the repository name, the README, the DOI record, and the SPASE record, all of
  which use `FitsFlow`.
- **"Browser-based FITS to ASDF pipeline | DOI: 10.5281/zenodo.17069413"** — the GitHub repository's
  `description` field. Checked and rejected: it is a short repository tagline, written to fit
  GitHub's one-line slot and carrying a DOI reference inside it, so it is neither the software's name
  nor a sentence. It was also weighed as a Field 9 concise description and rejected there (see
  Field 9).

### 8. Description (MANDATORY)
FitsFlow is a browser-based platform developed by the author to streamline the exploration and annotation of Solar Dynamics Observatory (SDO) FITS images through a fully integrated, cloud-native environment. The system connects heliophysics data services from Joint Science Operations Center (JSOC), Helioviewer, and the Heliophysics Event Knowledgebase (HEK), enabling users to parse FITS headers, align event times, and automatically retrieve associated imagery and metadata. The backend, deployed on Amazon Web Services (AWS) Lambda and Elastic Cloud Compute (EC2), handles on-demand processing and delivers all outputs through a lightweight web interface. FitsFlow produces structured, machine learning–ready outputs, including support for the Advanced Scientific Data Format (ASDF). Each session allows up to 170 MB of fits data and the results can be downloaded in bulk as a ZIP file containing: header metadata in JSON, pixel data in CSV and NumPy formats, colorized PNG images from Helioviewer, grayscale PNGs from JSOC, and HEK metadata in JSON format. These outputs are designed to support reproducible and interpretable ML workflows for classifying, segmenting, and forecasting solar events, laying the foundation for cyberinfrastructure that connects solar surface activity to radiation impacts in low Earth orbit (LEO). FitsFlow represents the first in a planned suite of “KISS” tools (Keep It Simple, Scientist) aimed at lowering the barrier to entry for machine learning in heliophysics. With browser-native visualization, downloadable structured examples, zero-install access, and no login required, FitsFlow broadens accessibility for researchers, educators, and citizen scientists working with solar data.

Carried over unchanged from the existing HSSI record. This is the author's own abstract, matching the
`descriptions[0].description` body of the DataCite record for the DOI and the "About" overlay text in
`client/js/fitsFlow.js` (`showOverlay('about')`) essentially word for word. It is preserved as
written: no rephrasing is warranted, and the two cosmetic irregularities it contains — the lowercase
"170 MB of fits data" and the typographic quotation marks around "KISS" — are reproduced from the
authoritative source rather than corrected, because they are the author's text and carry no factual
error. The repository confirms the factual claims: the 170 MB session cap is `let maxSizeMB = 170` in
`client/js/fitsFlow.js`, and the ZIP contents listed match `createZipFromPlaylist()`'s fetch list
(headers, hek, asdf, images/sdo, images/jsoc, data CSV, data NPY).

### 9. Concise Description (OPTIONAL)
FitsFlow is a browser-based application that takes a solar FITS image and returns machine-learning ready outputs.

**This corrects a previously stored value.** The earlier value was:

```
FitsFlow is a browser-based application that takes a solar FITS image and returns machine-learning ready outputs.

Abstract
```

Its trailing blank line and bare word `Abstract` were a DataCite/Zenodo autofill artifact, not
authored text. The description deposited for this DOI begins `FitsFlow v0.1.0` / `Abstract` /
`FitsFlow is a browser-based platform…`, and the autofill captured the opening summary sentence
together with the `Abstract` section heading that immediately followed it. The heading was therefore
removed as a mechanical defect rather than as an editorial preference: the author's sentence is
unchanged, including her hyphenation "machine-learning ready". 113 characters, within the field's
200-character limit. Recorded so the stray heading is recognised as an artifact and not restored if
it is met again in a DOI-derived source.

Corroboration that the sentence itself is the intended concise description: it is the README's own
one-line summary (line 3) and the opening line of the GitHub release notes for v.0.1.0. The README
spells it "machine learning ready" without the hyphen; the hyphenated form is kept, because choosing
between two equivalent renderings of the author's own sentence is not this file's business.

Also considered and rejected: **"Browser-based FITS to ASDF pipeline | DOI: 10.5281/zenodo.17069413"**,
the GitHub repository's `description` field. It is accurate and admirably short, but it is a
repository tagline rather than a description — it embeds a DOI reference that duplicates Field 2, and
it drops what makes the tool distinctive (browser-based, no install, ML-ready outputs). The author's
own one-line summary is the stronger evidence and the stronger preview text.

### 10. Publication Date (RECOMMENDED)
2025-09-06

Carried over from the existing HSSI record and confirmed by four independent sources: DataCite
`dates: [{"date": "2025-09-06", "dateType": "Issued"}]`; the DataCite record's own
`created`/`registered` timestamps of `2025-09-06T18:04:27Z`; the GitHub release `published_at` of
`2025-09-06T18:04:21Z`; and the SPASE record's `PublicationDate 2025-09-06 00:00:00Z` and
`ReleaseDate 2025-09-06 18:11:28`. Since v.0.1.0 is the first and only release, this date is also the
correct version date (Field 12).

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

Carried over from the existing HSSI record. Correct per Field 11's rule that Zenodo is the publisher
for a DOI obtained through the GitHub–Zenodo workflow, which is what happened here: the README badge
is `https://zenodo.org/badge/1044586127.svg`, the GitHub-repository badge ID form. DataCite's
`publisher` is `Zenodo` and the SPASE record's `PublishedBy` is `Zenodo`. The stored identifier is
the plain URL rather than a ROR, which is exactly the fallback Field 11 documents (and the example it
gives is this very URL).

### 12. Version (RECOMMENDED)
- **Version Number:** v.0.1.0
- **Version Date:** 2025-09-06
- **Version PID:** `https://doi.org/10.5281/zenodo.17069414`
- **Version Description:** as stored, unchanged (reproduced verbatim below)

**v.0.1.0 is the latest release available now.** The evidence, gathered against the pinned revision:

- The repository has exactly one git tag, `v.0.1.0`, pointing at commit
  `96f0238e8ad90194e752e5267ea83dd7b2bf25cd`.
- The GitHub releases API returns exactly one release: tag `v.0.1.0`, name "Initial Release",
  `published_at 2025-09-06T18:04:21Z`, not a draft and not a prerelease.
- The concept DOI `10.5281/zenodo.17069413` has exactly one version child. DataCite reports a single
  `HasVersion` relation, to `10.5281/zenodo.17069414`, whose `version` attribute is `v.0.1.0` and
  whose `IsVersionOf` points back to the concept DOI. There is no second Zenodo deposit, so no newer
  release exists to adopt.
- DataCite's `version` attribute on both DOIs is the string `v.0.1.0`, matching the stored number
  including its unusual dot after `v`. That punctuation is the author's; it is preserved rather than
  normalised to `v0.1.0`.
- The 16 commits between the tag and the pinned revision `6111c361` change `README.md` (+39/−4),
  delete two stale duplicate files (`client/README.md`, and `client/index.html` — the live page is
  `client/html/index.html`), add `ff_logo.png`, and edit
  `server/lambda_layers/layer_urls.md`. **No functional source file changed after the release**, so
  v.0.1.0 still accurately describes the current code and no unreleased-work caveat is needed.

**The version date corrects a previously stored value.** `2025-09-08` was stored; every
authoritative source says `2025-09-06`:

| Source | Value |
|---|---|
| GitHub release `published_at` | `2025-09-06T18:04:21Z` |
| Tag commit `96f0238e` author date | `2025-09-06 14:01:16 -0400` (= 18:01:16 UTC) |
| DataCite `dates[].Issued` for 17069414 | `2025-09-06` |
| DataCite `created` / `registered` for 17069414 | `2025-09-06T18:04:26Z` / `2025-09-06T18:04:27Z` |
| SPASE `ReleaseDate` | `2025-09-06 18:11:28` |
| HSSI's own Field 10 publication date | `2025-09-06` |

`2025-09-08` was also internally inconsistent with this record's own publication date, for a package
whose only release *is* its publication. The likeliest origin of the stray date is the README commit
`7e9ad67` of 2025-09-08 — a documentation edit two days after the release, not a release event. Two
further dates in this vicinity are recorded so none of them is mistaken for the release later: the
SPASE record carries a `RevisionEvent ReleaseDate 2025-09-12` annotated "Initial release of FitsFlow
v0.1.0", which is the date the SPASE description itself was revised; and the repository's most recent
commit, 2026-07-14, is a README edit and not a release either.

The version description is retained exactly as stored. It is the author's v.0.1.0 release note as
deposited on Zenodo, and rewriting it is not this file's business. Its exact text is on record here,
because two of its details are found nowhere else (see the note that follows it):

```
FitsFlow v0.1.0

FitsFlow is a browser-based application that takes a solar FITS image and returns machine-learning ready outputs.

Abstract

FitsFlow is a browser-based platform developed by the author to streamline the exploration and annotation of Solar Dynamics Observatory (SDO) FITS images through a fully integrated, cloud-native environment. The system connects heliophysics data services from Joint Science Operations Center (JSOC), Helioviewer, and the Heliophysics Event Knowledgebase (HEK), enabling users to parse FITS headers, align event times, and automatically retrieve associated imagery and metadata. The backend, deployed on Amazon Web Services (AWS) Lambda and Elastic Cloud Compute (EC2), handles on-demand processing and delivers all outputs through a lightweight web interface. FitsFlow produces structured, machine learning–ready outputs, including support for the Advanced Scientific Data Format (ASDF). Each session allows up to 170 MB of fits data and the results can be downloaded in bulk as a ZIP file containing: header metadata in JSON, pixel data in CSV and NumPy formats, colorized PNG images from Helioviewer, grayscale PNGs from JSOC, and HEK metadata in JSON format. These outputs are designed to support reproducible and interpretable ML workflows for classifying, segmenting, and forecasting solar events, laying the foundation for cyberinfrastructure that connects solar surface activity to radiation impacts in low Earth orbit (LEO). FitsFlow represents the first in a planned suite of “KISS” tools (Keep It Simple, Scientist) aimed at lowering the barrier to entry for machine learning in heliophysics. With browser-native visualization, downloadable structured examples, zero-install access, and no login required, FitsFlow broadens accessibility for researchers, educators, and citizen scientists working with solar data.

Simple Language

In simple terms:



You upload a FITS file in your browser.

FitsFlow automatically connects to NASA/NOAA data services (HEK, JSOC, Helioviewer).

The system processes everything in the cloud.

You get back a single manifest file and outputs (images, metadata, ASDF).


FitsFlow connects all the dots so researchers, educators, and the public can use solar data without special software.

System Overview



AWS services: Lambda, API Gateway, S3, CloudFront, Route 53, CloudWatch, EventBridge, EC2

External APIs: HEK, JSOC, Helioviewer

Outputs: images, metadata, ASDF, manifest files


Click here to view the AWS flow of information!

Click here to view a demo!

Repository Structure



client/ – frontend code (HTML, CSS, JS, assets)

server/ – backend AWS Lambda functions, IAM policies, layers, API definitions

README.md – documentation (system architecture, data flow, security, future work)


Research Outputs



Dragon Con 2025 — Space & Science Tracks

Science and Cyberinfrastructure for Discovery 2025 — Session 4: Lightning Talks

Data, Analysis, and Software in Heliophysics 2025 — (session details pending)

AGU Fall Meeting 2025 — Session SH032: The Long Way: Heliosphere Modeling with Operations in Mind


Version Info



Release type: First public release

Tag: v0.1.0

License: Apache-2.0
```

Two details in that release note are worth flagging for a future refresh, since they are *not*
errors to correct here but do carry information the current README no longer does: it lists a fourth
research output ("AGU Fall Meeting 2025 — Session SH032") absent from the README, and it names
CloudWatch and EventBridge among the AWS services where the README's list omits them.

### 13. Programming Language (RECOMMENDED)
- Javascript
- Python 3.x

Both carried over from the existing HSSI record and confirmed; both are exact controlled values —
note the controlled spelling `Javascript`, not `JavaScript`.

GitHub's language statistics give JavaScript 63,141 bytes, Python 29,541, CSS 18,662, HTML 16,002,
so JavaScript and Python are not merely present but dominant. Python 3 specifically is confirmed by
the `AWSSDKPandas-Python310` layer ARN (Python 3.10 runtime) and by f-strings throughout
`server/lambda_functions/`.

Considered and not added: **CSS** and **HTML**, which the author's own SPASE record lists under
`CodeLanguage` ("HTML, CSS, JavaScript, Python") and which GitHub reports by byte count. Neither is a
programming language and neither has a controlled value of its own; Field 13 also states explicitly that
the list "is not meant to be an exhaustive list" but the "most important languages". The two stored
values are the right two.

### 14. Reference Publication (RECOMMENDED)
Not found.

There is no publication describing FitsFlow. Verified rather than assumed: the README's only DOI is
the Zenodo software badge; DataCite's `relatedIdentifiers` for both the concept and version DOIs
contain no `IsDescribedBy`, `IsSupplementedBy`, or `IsReferencedBy` relation (only
`IsSupplementTo https://github.com/indiajacksonphd/FitsFlow/tree/v.0.1.0` and the concept/version
pair); there is no `CITATION.cff` and no "how to cite" section beyond the badge; and the SPASE record
carries no `InformationURL` to a paper. There is no JOSS submission. The NSF award's public abstract
is a funding record, not a publication, and does not belong here.

If a software paper or a DASH/AGU abstract with a DOI appears later, this is the field for it.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** `https://spdx.org/licenses/Apache-2.0`

The licence is unambiguous; every available source agrees, so there is nothing to weigh:

- `LICENSE` in the repository root is the verbatim 201-line Apache License, Version 2.0 text.
- The GitHub API reports `license.spdx_id: "Apache-2.0"`, `license.name: "Apache License 2.0"`.
- DataCite's `rightsList` for both DOIs is
  `{"rights": "Apache License 2.0", "rightsIdentifier": "apache-2.0", "rightsIdentifierScheme": "SPDX", "rightsUri": "http://www.apache.org/licenses/LICENSE-2.0"}`.
- The GitHub release notes for v.0.1.0 state "License: Apache-2.0".

`Apache License 2.0` is the exact controlled value and is also the SPDX title, so no approximation
was needed. The recorded URI is the canonical SPDX URI for that licence. DataCite's `rightsUri`
(`http://www.apache.org/licenses/LICENSE-2.0`) points at the same licence text by a different URL and
is deliberately not used: Field 15 prefers SPDX-supported licences, and the SPDX URI is this
licence's canonical identifier.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- machine learning
- cloud computing
- serverless
- aws
- asdf
- solar imaging
- image processing
- extreme ultraviolet
- solar dynamics observatory
- sdo
- heliophysics
- open science
- citizen-science
- metadata

All fourteen are recorded in exactly the lower-case forms listed above. (HSSI displays keywords in
Title Case while the recorded values are lower-case, so compare them on the normalised form rather
than on appearance.)

Why these: the set favours concepts that no other field can express. `machine learning`,
`cloud computing`, `serverless`, and `aws` capture what makes FitsFlow unusual in HSSI — a
zero-install, browser-native, AWS-Lambda-backed pipeline whose stated purpose is producing ML-ready
data — and none of that is expressible through Functionality, Region, or Phenomena. `asdf` is
important because the Advanced Scientific Data Format is FitsFlow's headline output and **no specific
controlled File Format value represents ASDF**, so without this keyword an ASDF search cannot find it
(Field 19 can only say `Other`). `solar dynamics observatory` and `sdo` are both included
deliberately: the abbreviation is what users type and the full name is what a curator would look for.
`extreme ultraviolet` names the AIA channel regime, which no Region or Phenomena value covers. `open science` and `citizen-science` reflect the explicit
design goals — no login, no install, downloadable examples, "researchers, educators, and citizen
scientists" — and `metadata` reflects that header and HEK metadata handling is the product, not a
side effect.

Deliberately **not** used: a **malformed controlled value** exists,
`space weather, heliophysics, artificial intelligence, machine learning, cloud computing, python, amazon web services`
— a single un-split comma-delimited string whose content overlaps this software's subject matter
closely enough to be tempting. It is a data-quality artifact of an earlier submission and must never
be selected; the individual concepts it runs together are available as proper keywords and are used
above.

Considered and not selected because another field already carries them: `fits` (Field 18),
`magnetogram`, `corona`, `chromosphere`, `photosphere` (Fields 5 and 31), `solar physics` and `sun`
(redundant with `heliophysics` plus the Region values), and `web service` (conveyed by
`Data Visualization: Web-Based`). Also rejected: `flare detection` and `event detection` — FitsFlow
retrieves HEK's already-detected events and detects nothing itself.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- S3/Cloud-aware
- Other

All four are exact controlled-vocabulary terms.

- **HTTP/HTTPS Directories** — `get_closest_jsoc_url()` fetches an Apache directory index and scrapes
  it: `requests.get("https://jsoc1.stanford.edu/data/aia/images/{year}/{month}/{day}/{wavelength}/")`
  followed by `re.findall(r'href="([^"]+\.jp2)"', response.text)`, with the parallel HMI branch
  matching `href="(\d{8}_\d{6}_[A-Za-z_]+_4k\.jpg)"`. `daily_videos.build_url()` likewise composes
  `https://sdo.gsfc.nasa.gov/assets/img/dailymov/{y}/{m}/{d}/{date}_1024_{wave}.mp4`. This is
  literal HTTPS-directory traversal, not an API call.
- **Observatory/Mission-specific** — JSOC (`jsoc1.stanford.edu`) is SDO's Joint Science Operations
  Center and `sdo.gsfc.nasa.gov` is the SDO mission site; both are mission-specific archives, and
  FitsFlow reads nothing else of the kind. Field 17 instructs that an observatory-specific source be
  cross-listed by naming the mission in Related Observatories, which Field 32 does (Solar Dynamics
  Observatory).
- **S3/Cloud-aware** — the pipeline's working store is S3 throughout, via `boto3`:
  `s3.generate_presigned_url("put_object", ...)` for upload, `s3.list_objects_v2` +
  `s3.download_file` to stage FITS into the Lambda, `s3.get_object` to read back HEK JSON and header
  text when building the ASDF tree, `s3.put_object` for every product, and a paginated
  `s3.delete_objects` sweep in the nightly cleaner.
- **Other** — for the two primary services that no specific controlled value represents: the
  Helioviewer API v2
  (`api.helioviewer.org/v2/getClosestImage/`, `/v2/downloadImage/`) and the Heliophysics Event
  Knowledgebase, queried through Helioviewer's event endpoint as
  `api.helioviewer.org/v2/events/?startTime=…&endTime=…&sources=HEK`. Both are named as first-class
  supported sources in the app's own "Supported Data" panel.

Considered and rejected: **The Virtual Solar Observatory.** (not used anywhere — FitsFlow reaches
JSOC and Helioviewer directly), **CDAWeb**, **HAPI**, **OMNIWeb**, **SSCWeb**, **AMDA**, **das2**,
**Madrigal**, **VirES**, **TAP**, **GFZ**, **WDC** (none appears in the code or documentation), and
**FTP/FTPS Directories** (every retrieval is HTTPS).

### 18. Input File Formats (RECOMMENDED)
- FITS

Carried over unchanged from the existing HSSI record, and confirmed to be the complete list of
formats a user can supply. `client/html/index.html` restricts the picker to
`<input type="file" id="fitsUpload" multiple accept=".fits">`; the change handler enforces
`if (!file.name.toLowerCase().endsWith('.fits')) continue`; and the server side only ever collects
`if key.endswith(".fits")`. Files that open but are not SDO products are rejected downstream on
`TELESCOP`, so the accepted input is narrower than FITS in general, never wider.

Considered and **not** added, deliberately: **JSON** and **Other**. FitsFlow does read other formats
— it parses HEK JSON responses, reads back its own `_hek.json` and `_header.txt` intermediates from
S3 when assembling the ASDF tree, loads the `helioviewer_source_id.json` lookup table, and decodes
JPEG 2000 and JPEG browse images through Pillow. None of those is an *input format the software
supports* in the sense this field means: they are FitsFlow's own retrievals from the services it
queries and its own intermediate products, and the services are recorded in Field 17 instead. Adding
them would make an HSSI search for `input format: JSON` return a tool that accepts only FITS.

### 19. Output File Formats (RECOMMENDED)
- ascii
- csv
- JSON
- Other

`csv`, `JSON`, and `Other` come from the existing HSSI record; `ascii` accompanies them for the
reason given below. All four are exact controlled-vocabulary terms.

- **csv** — `s3.put_object(..., Key=f"temp/{session_id}/processed/data/{fname}_data.csv", Body=df.to_csv(index=False))`.
- **JSON** — the HEK event metadata is written as `json.dumps(data, indent=2)` to
  `.../hek/{fname}_hek.json`.
- **ascii** — added because the FITS header is emitted as plain text, not JSON:
  `header_txt = "\n".join([f"{k} = {v}" for k, v in header.items()])` written to
  `.../header/{fname}_header.txt`, and the download bundle also contains a generated plain-text
  `README.txt` manifest. The generated manifest itself says "headers/ — FITS header metadata in plain
  text". Worth noting for a future maintainer: both the HSSI description and the app's "Data Types"
  table say the header is delivered as JSON, but the code writes `.txt`; `ascii` records what the
  software actually produces, and the descriptive text is left as the author wrote it.
- **Other** — for the four output formats that no specific controlled File Format value represents:
  NumPy `.npy`
  (`np.save(npy_buffer, data)`), PNG (both the Helioviewer colourised image and the JSOC greyscale
  image re-encoded via Pillow), ASDF (`asdf.AsdfFile(tree).write_to(...)`, the headline ML-ready
  product), and the client-assembled ZIP bundle. The nightly `.mp4` stitched SDO movie is also
  covered here.

Considered and rejected: **FITS** — FitsFlow never writes FITS. The uploaded file is referenced by
relative path inside the ASDF tree (`"fits_file": f"./{fname}.fits"`) and the local copy is deleted
after processing (`os.remove(file_path)`); no FITS file is generated. **HDF5** — considered only
because ASDF and HDF5 are often confused; ASDF is a YAML-tree-plus-binary-blocks format and no
`h5py`/HDF5 code exists here. **netCDF3/4**, **CDF**, **Zarr**, **IDL.sav**, **ISTP-Compliant** — no
evidence of any.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

Carried over unchanged. `Operating System Independent` is the exact controlled-vocabulary term, spelled
out in full — `OS Independent` is not a value in this vocabulary and would be rejected. The user-facing
software is a web page: the SPASE record's `ExecutionEnvironment`
gives `OperatingSystem: Platform-independent (requires modern web browser: Chrome, Firefox, Safari)`
and `Prerequisites: Modern web browser (Chrome, Firefox, Safari), internet connection`, with
`ApplicationInterface: GUI`. There is nothing to install.

Considered and rejected: adding **Linux**. The server side genuinely is Linux-specific — the Lambda
layers were "built on Amazon Linux EC2 to ensure binary compatibility with the AWS Lambda runtime
(Amazon Linux 2)". But that is the maintainer's deployment target, not an operating system a user
installs FitsFlow on, and listing it alongside `Operating System Independent` would be
self-contradictory. The only user requirement is a browser.

The single real platform constraint is a screen-size gate, not an OS one: `checkMobileView()`
activates a `mobile-blocker` overlay below 600 px ("Mobile View Not Supported...Yet"). That is why
`MobilePlatform` is not selected.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Carried over unchanged; `CPU Independent` is the exact controlled-vocabulary term. All computation happens server-side on AWS
Lambda, so the client's architecture is irrelevant and nothing is compiled for the user's machine.
`GPU` is rejected — despite the ML-ready framing there is no ML model, no CUDA, and no accelerator
code anywhere. `HPC or HEC` is rejected for the same reason as `High Performance Computing` in
Field 4.

### 22. Related Phenomena (OPTIONAL)
- Coronal Heating
- Solar Corona
- Solar Flares

All three carried over unchanged from the existing HSSI record, and all three are exact
controlled-vocabulary terms. The Phenomena vocabulary is flat and **closed**: a phenomenon with no
term of its own belongs in Keywords (Field 16), not here.

Repository support for each: **Solar Flares** is the strongest — the app's own data-source table
describes HEK as supplying "Flare and event metadata", `fetch_hek_events()` retrieves HEK records
around each observation time, and the AIA channel table names flares for 94 ("Hot flaring regions"),
131 ("Flares & hot plasma"), and 193 ("Corona & flaring regions"). **Solar Corona** follows from the
six coronal AIA channels FitsFlow supports. **Coronal Heating** is the science question that the
supported channel set is built to address (94 at ~6.3 MK, 171 at ~0.6 MK, 211 at ~2 MK, 335 at
~2.5 MK — a temperature ladder across quiet corona and active regions); it is the submitter's
selection, it is defensible, and nothing contradicts it, so it is retained.

Considered and **not** selected: **Coronal Mass Ejections.** The case for it is real but thin —
`fetch_hek_events()` passes only `sources=HEK` with no event-type filter, so CME records genuinely can
appear in the returned JSON, and the shipped AIA 304 example is "a dramatic prominence eruption."
Against it: the repository never claims CME support, there is no CME-specific handling, and the
unfiltered query would equally justify every event type HEK catalogues. Left out as a matter of
record, not oversight. **X-ray emission** is rejected because AIA and HMI observe EUV, UV, and
visible light, not X-rays. **Geomagnetic Storms** and **Solar Wind** have no basis at all here.

### 23. Development Status (RECOMMENDED)
Active

`Active` is the exact controlled-vocabulary term, and the bare term is the whole value.
repostatus.org defines it as "The project has reached a stable, usable state and is being actively
developed."

Both halves of that definition hold. *Stable and usable*: v.0.1.0 is a tagged, released, DOI-minted
public version, and `https://www.fitsflow.org` is a live production deployment serving the
application, with a working logo asset and downloadable example bundles. *Actively developed*: the
repository's most recent commit is 2026-07-14, three weeks before this extraction; the repository is
neither archived nor disabled and carries no open issues; and the funding award runs to 2027-01-31.

Considered and rejected: **WIP** — its definition requires that there be no stable public release
yet, and there is one. **Inactive** and **Unsupported** — contradicted by commits eleven months after
release and by an award still running. **Concept** — this is a deployed production service, not a
proof of concept. Note for a future refresh: the commits since the release are documentation-only, so
if the pattern continues with no functional change, `Inactive` may eventually become the more honest
term. It is not yet.

### 24. Documentation (RECOMMENDED)
`https://github.com/indiajacksonphd/FitsFlow`

Carried over unchanged. The repository README *is* the documentation, and a substantial one: system
architecture diagram, data flow, security model, web-accessibility categorisation, threat model,
future work, research outputs, and acknowledgements, with `server/README.md` covering every AWS
service, `server/iam_policies/` documenting all six IAM/CORS configurations, `server/apis/README.md`
covering both backend entry points, and `server/lambda_layers/layer_urls.md` covering the dependency
layers. There is no `docs/` directory, no Read the Docs configuration, and no GitHub Pages site, so
no dedicated documentation host exists to point at instead. Field 24 explicitly permits reusing the
access URL when they are the same.

Considered and rejected: **`https://www.fitsflow.org`.** The live app does carry explanatory content
in its overlays (About, Spacecraft, Supported Data, Sample Downloads) and the SPASE record lists it
as the `Installer URL`, but it offers no installation or technical documentation — that is what the
README provides. Rejected as well: the YouTube demo `https://youtu.be/6J0IHxmNrg8` (a video walk-
through, not documentation) and the repository's GitHub wiki, which is enabled but empty.

One durable caveat for a future maintainer: the README's "Section 2 — Client Side" link points to
`client/`, whose `README.md` was deleted in commit `d1bc661`, so that link now lands on a bare
directory listing. The "Section 3 — Server Side" link still resolves to `server/README.md`. This is
an upstream README defect, not a wrong value for this field.

### 25. Funder (OPTIONAL)
- **Organization:** U.S. National Science Foundation
  **Funder Identifier:** `https://ror.org/021nxhr62`

Carried over unchanged from the existing HSSI record and confirmed correct. `https://ror.org/021nxhr62`
is the National Science Foundation's ROR, and `U.S. National Science Foundation` is the current ROR
display name — which also satisfies Field 25's instruction to avoid acronyms, where a bare "NSF"
would not. DataCite's `fundingReferences[0]` gives `funderName: "U.S. National Science Foundation"`
with `funderIdentifier: 10.13039/100000001` (the Crossref Funder ID for the same body); the ROR is
the identifier type this field prefers, so the stored value stands. The README's acknowledgement
("supported by the National Science Foundation (NSF) Atmospheric and Geospace Sciences Postdoctoral
Fellowship"), the app sidebar ("National Science Foundation"), and the SPASE record's
`Funding/Agency: National Science Foundation` all agree that NSF is the sole funder.

No second funder exists. The SPASE acknowledgement additionally thanks Georgia State University's
Solar Informatics and Data Mining Lab and credits data and services from Helioviewer, HEK, JSOC, and
the Python in Heliophysics Community — none of which is a financial contributor, so none belongs
here.

### 26. Award Title (OPTIONAL)
- **Award Title:** Postdoctoral Fellowship: AGS-PRF: Advancing Heliophysics with Automated Machine Learning and Open-Source Integration
- **Award Number:** 2444918

Both sub-fields are carried over unchanged from the existing HSSI record, and both were already
correct and complete. That is worth stating plainly, because **HSSI's rendered display of an award
shows only its title and omits the award number**, so a number that is recorded looks absent. The
number here was recorded all along — anyone reading only the rendered form should not conclude
otherwise, and should not treat this field as a gap to fill.

The award is confirmed against the authoritative NSF record for award 2444918: title
"AGS-PRF: Advancing Heliophysics with Automated Machine Learning and Open-Source Integration",
program "Postdoctoral Fellowships" in the Division of Atmospheric and Geospace Sciences, PI India
Jackson, performing organization Georgia State University, 2025-02-15 to 2027-01-31, \$202,000,
`transType: Fellowship Award`. The number also appears in the README acknowledgement ("AGS-PRF Award
#2444918"), in the app sidebar ("Award Number: 2444918-AGS-PRF"), in the ASDF metadata block written
by every run (`"nsf_award": "AGS-PRF #2444918"`), in the generated bundle manifest ("Award Number:
NSF AGS-PRF #2444918"), in DataCite's `fundingReferences[0].awardNumber`, and in the SPASE record's
`AwardNumber`.

On the title, the stored value is retained rather than replaced by NSF's shorter one. The stored
string is DataCite's `fundingReferences[0].awardTitle` verbatim — the author's own deposit — and it
is NSF's official title with the program name prefixed, so it is a superset rather than an error;
Field 26 asks for the full award title, and no factual claim in it is wrong. Two alternatives were
considered and rejected: NSF's bare title (drops the fellowship-programme context the author chose to
include) and the SPASE record's `Project` value, which is the same bare NSF title.

Length constraint recorded because it is a real hazard for this particular value: the stored title is
116 characters and `Award.name` is a 128-character CharField that fails at the database write rather
than at serializer validation. 116 fits, with only 12 characters of headroom — so any future
expansion of this title (adding "National Science Foundation" or the award number to the string, for
instance) would exceed the cap and must not be attempted.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found.

This is a considered "none", not an unexamined blank. The README's "Research Outputs" section lists
three 2025 presentations, and the stored v.0.1.0 release note lists a fourth. Each was evaluated
against Field 27's requirement of a DOI, or failing that an APA citation with a permanent link, and
each was rejected:

- **Dragon Con 2025 — Space & Science Tracks.** The link is a conference-app speaker page
  (`app.core-apps.com/dragoncon25/speakers/aadbab04df55073681678e0c579dbd8d`). A speaker profile in
  an event app is neither a publication nor a permanent link — such apps are retired after the
  convention — and Dragon Con is a fan convention with a science programming track, not a venue with
  a published proceedings.
- **Science and Cyberinfrastructure for Discovery 2025 — Session 4: Lightning Talks.** The link
  (`arctic.gsu.edu/training/scd/#lightning-talks`) is a workshop agenda anchor, not a record of a
  specific work. No abstract identifier, no proceedings.
- **Data, Analysis, and Software in Heliophysics 2025 — Open Oral Session.** The link
  (`dash2025.space.swri.edu/#agenda`) is a meeting agenda anchor. DASH does not mint abstract DOIs,
  and the stored release note describes this same item as "(session details pending)".
- **AGU Fall Meeting 2025 — Session SH032.** Named only in the stored version description, not in the
  README. `SH032` identifies a *session*, not an abstract, so there is nothing citable even in
  principle; AGU abstract identifiers are per-abstract.

None of the four yields a DOI or a durable citation, so listing any of them would put an agenda URL
where a publication identifier belongs. If the author later obtains an AGU abstract DOI, a
proceedings paper, or a JOSS paper, this field (and Field 14 for a describing paper) is where it
goes.

### 28. Related Datasets (OPTIONAL)
Not found.

FitsFlow's dataset relationship is real but is expressed by other fields: the SDO AIA and HMI
instruments in Field 31, the Solar Dynamics Observatory in Field 32, and the JSOC/Helioviewer/HEK
sources in Field 17. Field 28 wants a dataset DOI, or an APA citation with a permanent link, and no
such identifier exists in any source here.

What was examined and rejected:

- **The JSOC series `aia.lev1_euv_12s`,** which appears in a live export link in the app's Supported
  Data panel (`jsoc.stanford.edu/ajax/exportdata.html?ds=aia.lev1_euv_12s[2020-01-01T00:00:00/20m][131]`).
  It is a genuine named data series, but it is used there as a clickable illustration of where to get
  a FITS file, and JSOC series names are not persistent identifiers.
- **The HMI continuum and magnetogram browse products** under
  `jsoc1.stanford.edu/data/hmi/images/`, and the SDO daily movies under
  `sdo.gsfc.nasa.gov/assets/img/dailymov/` — directory paths, not identified datasets.
- **FitsFlow's own example bundles** at `fitsflow.org/examples/05-01-2013-304/0304.zip` and
  `fitsflow.org/examples/collection/collection.zip`. These are demonstration outputs the software
  generated, not datasets it supports, and they carry no identifier.

Negative research worth preserving so it is not repeated: `hpde.io` cannot be used to confirm an SDO
dataset identifier by URL probing. It returns HTTP 200 with an empty body for a plausible path such
as `hpde.io/VSO/NumericalData/SDO/AIA/Lev1.html` **and** for a deliberately invented path, so a 200
there is not evidence a record exists. Any future attempt to add an SDO dataset here needs a record
confirmed by content, not by status code.

### 29. Related Software (OPTIONAL)
None. This field is deliberately empty.

**A previously stored value was removed: `https://www.fitsflow.org/`.** That URL is FitsFlow's own
live deployment, not other software. Field 29 is for software that performs similar tasks, a
predecessor or fork parent, a companion package, or a domain-specific dependency — in every reading,
*other* software, so a project's own deployment URL cannot qualify.

The counter-argument was weighed and rejected rather than overlooked. HSSI has no "access URL" or
"homepage" field, and the author's SPASE record lists this same URL as its `Installer URL`, so the
value was plausibly the submitter's workaround for recording where the application runs. Correctness
was chosen over retaining it: a self-reference in a related-software field misinforms every reader
and every downstream consumer, whereas the access link is recoverable from the SPASE record and from
the README, which links `https://www.fitsflow.org` directly. Field 24 independently carries the
repository URL. Recorded so the URL is not re-added here when it is met again in a source.

**HelioCloud was considered and deliberately not added.** The author's own SPASE record states
FitsFlow was "inspired by HelioCloud", and HelioCloud is a genuinely comparable thing: an AWS-based
cloud platform for heliophysics data and analysis, which would make it a "performs similar tasks /
predecessor in spirit" candidate rather than a dependency claim. It was not added for two reasons.
"Inspired by" in an acknowledgement is too soft to carry a similar-purpose assertion — it records
influence on the author, not a relationship a user could act on. And HelioCloud has no canonical
repository URL to cite: the GitHub organisation is `https://github.com/heliocloud-data`, whose core
platform repository is now named `platform-legacy`, alongside `heliocloud_tools`, `cloudcatalog`,
`runtimes`, and `science-tutorials`. Recorded with its reasoning so a future agent does not
re-propose it on the same evidence; a stated similar-purpose relationship, or a stable HelioCloud
repository URL, would be new evidence worth reconsidering.

Considered and rejected, with reasons, so they are not re-proposed:

- **Helioviewer, JSOC, and HEK.** FitsFlow depends on all three absolutely, but it consumes them as
  *hosted data services* over HTTP, not as software packages it links against. They are recorded in
  Field 17 (Data Sources) where they belong. The Helioviewer Project's API server is itself open
  source, so the relationship could in principle be expressed at the software level — but FitsFlow's
  dependency is on the hosted endpoint rather than on that code, which makes Field 17 the accurate
  home for it.
- **astropy.** Tier B, and the bar is not met. `astropy.io.fits` is used internally to open and
  repair FITS files (`fits.open`, `hdul.verify('fix')`, `header.cards`, `astropy.io.fits.card.Undefined`);
  that is internal use of a FITS reader, not a demonstrated exchange of data models or an adapter API
  between peer tools.
- **asdf.** Tempting, because ASDF output is FitsFlow's headline product and a downstream user does
  read it back with the `asdf` library — but the library is used here as a serializer to write a file,
  which is a format relationship rather than a tool-to-tool interoperation. The format is instead
  surfaced through Field 19 (`Other`) and the `asdf` keyword in Field 16.
- **boto3, numpy, pandas, Pillow, requests, python-dateutil, ffmpeg** (server side) and **jQuery,
  JSZip, FileSaver.js, flatpickr** (client side, all CDN-loaded). Generic infrastructure — cloud SDK,
  arrays, dataframes, image codecs, HTTP, date parsing, media transcoding, DOM and file-download
  plumbing. Every one would be equally at home in a web app, a finance model, or a biology pipeline,
  so none says anything about this software.
- **SunPy.** The obvious similar-purpose heliophysics package for solar FITS handling, and therefore
  worth explicitly ruling out: FitsFlow does not use, mention, or reference SunPy anywhere. Listing it
  on thematic similarity alone would be invention.
- **The Python in Heliophysics Community.** Thanked in the SPASE acknowledgement, but PyHC is a
  community, not software. Worth recording alongside it, since it is the natural next question:
  **FitsFlow is not a PyHC package.** It appears in none of PyHC's three package registries — core,
  community, or unevaluated — so no curated PyHC metadata exists to draw on for any field in this
  file. Absence from PyHC is normal for a tool like this and is not a defect.

### 30. Interoperable Software (OPTIONAL)
None. This field is deliberately empty, and no replacement value was substituted.

**A previously stored value was removed: `https://spase-metadata.org/NSF/Software/FitsFlow.html`.**
That URL is FitsFlow's own SPASE resource description — `spase://NSF/Software/FitsFlow`, which names
FitsFlow as its `ResourceName` and carries this very DOI. No reading makes software interoperate with
its own metadata record, so unlike the Field 29 value this one had no plausible submitter intent to
weigh against removal. Recorded so it is not re-added here if it is met again in a source.

The SPASE record itself remains genuinely useful metadata, just not metadata for this field: it
exists, is maintained by the author, resolves at both
`https://spase-metadata.org/NSF/Software/FitsFlow` and the `.html` form, and independently
corroborates several values in this file (release date 2025-09-06, award number 2444918,
platform-independent execution environment, GUI interface, Zenodo as publisher, and India Jackson as
sole author and technical contact).

The field is empty because FitsFlow demonstrates no exchange with a peer heliophysics tool: there is
no shared or converted data model, no adapter or converter API, no plugin relationship, no companion
package, and no cross-language bridge. Its interface to the outside world is HTTP calls to three
hosted services (Field 17) and a downloadable output bundle. Everything considered for Field 29 was
considered here first and rejected for the same or stronger reasons — in particular **`astropy` and
`asdf`, which are Tier B packages used internally as format libraries with no cited data exchange**:
`astropy.io.fits` reads and repairs the uploaded FITS, and `asdf` serialises the output bundle, but
neither constitutes an exchange between peer tools that a user deliberately combines.

### 31. Related Instruments (OPTIONAL)
1. **Atmospheric Imaging Assembly**
   - Instrument Identifier: `https://spase-metadata.org/SMWG/Instrument/SDO/AIA`
2. **HMI**
   - Instrument Identifier: `https://spase-metadata.org/SMWG/Instrument/SDO/HMI`

Each instrument resolves unambiguously to the SPASE identifier shown above, once the `.html`
duplicate described below is set aside, and each name is copied verbatim from the matched controlled
entry.

Fields 31 and 32 require canonical SPASE identifiers, which is why every entry here and in Field 32
carries an `https://spase-metadata.org/` identifier beside its name. An instrument or observatory that
cannot be resolved to such an identifier must be omitted and documented rather than recorded as a bare
name.

`Atmospheric Imaging Assembly` appears under two identifiers — `.../SMWG/Instrument/SDO/AIA` (name
"Atmospheric Imaging Assembly", abbreviation `AIA`) and `.../SMWG/Instrument/SDO/AIA.html` (name
"Atmospheric Imaging Assembly (AIA)"). These are the same resource in bare and `.html` form, and the
bare identifier is the canonical one to record — a duplicate form of a single resource, not two
candidate instruments. Note also a genuine same-abbreviation controlled entry that is *not* this
instrument and must never be matched on abbreviation alone: `Magnetometers at Argentine Island`
(`.../IUGONET/Instrument/WDC_Kyoto/WDC/AIA/Magnetometer`), whose abbreviation is also `AIA`. The
identifier path segment `SDO/` is what disambiguates.

`HMI` resolves unambiguously to the SPASE identifier above. Its canonical name is the bare
abbreviation rather than "Helioseismic and Magnetic Imager", and the canonical name is copied verbatim
as required, so the value is `HMI` even though the fuller name reads better.

These two instruments — and only these two — are what FitsFlow is designed to support. The gate is
enforced in code, not merely documented:

- `process_fits_info()` rejects any file whose `TELESCOP` header does not contain `SDO`
  (`if "SDO" not in tele.upper(): ... continue`), with the browser reporting "All uploaded files were
  skipped — no SDO files detected."
- It then branches on `INSTRUME`: an `AIA` file requires `WAVELNTH` and is mapped through
  `wavelength_to_source`, built as
  `{int(entry["measurement"]): entry["source_id"] for entry in source_map if entry["observatory"] == "SDO" and entry["instrument"] == "AIA"}`;
  an `HMI` file is mapped through the parallel `content_to_source` comprehension filtered to
  `observatory == "SDO" and instrument == "HMI"`, translating `CONTENT` to `Ic` (continuum) or `M`
  (magnetogram). Anything else hits
  `Skipping: {fname} — Unsupported instrument: {instrument_raw}`.
- `get_closest_jsoc_url()` has exactly two branches, `"AIA" in instrument.upper()` and
  `"HMI" in instrument.upper()`, hitting instrument-specific JSOC paths
  (`/data/aia/images/…/{wavelength}/` and `/data/hmi/images/…`) and instrument-specific filename
  conventions.
- The supported channels are enumerated for the user in `client/html/index.html`: AIA 94, 131, 171,
  193, 211, 304, 335, 1600, 1700 (plus 4500 in the source map) and HMI Continuum / Magnetogram.

Both therefore pass the sanity check squarely: a user searching HSSI for `instrument:"AIA"` or
`instrument:"HMI"` should get FitsFlow back.

**Omitted with documentation — the eleven other instruments present in the repository.**
`server/lambda_functions/helioviewer_source_id.json` is a vendored copy of Helioviewer's source
catalogue with 39 entries covering GOES SUVI, PROBA2 SWAP, SOHO EIT, SOHO LASCO, SOHO MDI, STEREO-A
and STEREO-B COR1, COR2, and EUVI, in addition to SDO AIA and HMI. **None of the non-SDO entries is
used.** Both dictionary comprehensions that read the file filter on `observatory == "SDO"`, and the
`TELESCOP` gate rejects non-SDO files before the map is ever consulted, so these entries are
unreachable reference data — precisely the "platforms you could write a module for" that the relevance gate
excludes. This is recorded explicitly because a future agent grepping the repository will find eleven
recognisable instrument names in that file and would otherwise propose them all. Also excluded:
**SDO EVE**, which does have a canonical SPASE identifier (`.../SMWG/Instrument/SDO/EVE`) and belongs to the one
mission FitsFlow supports, but which the code never handles — EVE is a spectrometer producing
irradiance time series, not the imaging FITS FitsFlow processes.

### 32. Related Observatories (OPTIONAL)
1. **Solar Dynamics Observatory**
   - Observatory Identifier: `https://spase-metadata.org/SMWG/Observatory/SDO`

The mission resolves unambiguously to the SPASE identifier shown above, and its name is copied
verbatim from the matched controlled entry — the canonical name is the long form, not the
abbreviation "SDO".

FitsFlow is a single-mission tool, so this is the clearest association in the record. Beyond the
instrument-level gate described in Field 31, the mission is named throughout: the description and
README are about SDO FITS images; the app has a dedicated "Spacecraft" overlay devoted to SDO with
its AIA and HMI payloads and a NASA/SDO image credit; the nightly `daily_videos` job pulls SDO's own
daily movie products from `sdo.gsfc.nasa.gov`; the generated bundle manifest states the outputs are
"derived from NASA SDO Level 1 FITS files"; and Field 17's `Observatory/Mission-specific` selection
is cross-listed to exactly this entry, as Field 17 instructs.

Considered and **not** listed:

- **GOES, PROBA2, SOHO, STEREO-A, STEREO-B.** All five have canonical SPASE observatory identifiers
  and all five appear in `helioviewer_source_id.json`, but for the reason given in Field 31 the
  non-SDO entries in that file are unused reference data. Excluded deliberately.
- **JSOC, Helioviewer, and HEK.** These are data centres, services, and an event catalogue, not
  observatories, and none has an observatory identifier of its own. They are recorded in Field 17
  (Data Sources).
- **NOAA.** The README says FitsFlow "connects to NASA/NOAA data services (HEK, JSOC, Helioviewer)",
  but none of those three is a NOAA service — HEK is run by Lockheed Martin Solar and Astrophysics
  Laboratory, JSOC by Stanford, Helioviewer by NASA Goddard and partners. The NOAA mention is a
  README inaccuracy, and it is recorded here so it is not mistaken later for evidence of a GOES or
  NOAA association.

### 33. Logo (OPTIONAL)
`https://www.fitsflow.org/ff_logo_3.png`

Carried over unchanged from the existing HSSI record. Field 33 asks for a logo stored online in a
permanent, publicly accessible place, and the project's own domain qualifies.

One point worth recording, because it looks like drift and is not: the repository no longer contains
a file named `ff_logo_3.png`. Commit `d451540` (2025-10-08) deleted it and commit `b458d43` added
`ff_logo.png` in its place. The repository copy of `ff_logo.png` is 894,227 bytes — byte-for-byte the
same size as the asset the stored URL serves — so the image was renamed in the repository while the
deployed site kept the original filename. The stored URL is therefore still correct and should not be
"fixed" to point at the repository's raw file, which would be a less permanent link than the project
domain.
