# HSSI Metadata Extraction Results

**HSSI Software ID:** b5c250bc-fe00-41b8-b06b-2f4c3e688520
**Repository:** https://github.com/timduly4/pyglow
**Source Revision:** 1988757f3b6a4bd5ed98266a3fb1dc64f2513fc5
**Extraction Date:** 2026-09-10
**Validation Date:** 2026-09-11
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The repository does not identify the person who will submit or maintain this HSSI record.

### 2. Persistent Identifier (RECOMMENDED)

**Value:** Not found

The repository, its complete tracked history, its bundled archives, and its separate GitHub wiki provide no software DOI or other persistent identifier for pyglow. DataCite and Zenodo searches by the software title and capitalization variants, repository identity, subject/full text, and creator names found no record that identifies `timduly4/pyglow`. Broad `pyglow` matches instead describe pysat integrations, pysatMissions integrations, or research datasets that used a copy of pyglow. The package named PyGlow on PyPI is the unrelated `spino17/PyGlow` project and is not identifier evidence for this software.

### 3. Code Repository (MANDATORY)

**Value:** https://github.com/timduly4/pyglow

This is the repository URL declared in `setup.py`, linked by the PyHC registry, cited by the project wiki, and used by the CEDAR 2014 pyglow abstract.

### 4. Software Functionality (RECOMMENDED)

**Values:**

- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: Processing
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing

The public coordinate functions convert between WGS-84 latitude/longitude/altitude, Earth-centered Earth-fixed coordinates, and vertical/east/north vectors (`src/pyglow/coord.py`). `update_indices()` retrieves Kp/AP/F10.7 data from GFZ and Dst/AE data from WDC Kyoto, while the download helpers normalize source files for local use (`src/pyglow/indice_maintenance.py`). `Point` executes HWM, IGRF, IRI, and MSIS empirical climatologies, derives physical quantities, and computes 630.0-nm and 777.4-nm airglow volume emission rates; `Line` integrates along IGRF magnetic field lines (`src/pyglow/pyglow.py`).

The parent categories, coordinate transforms, data access, both field-line-tracing children, and empirical models are directly supported. `Analysis` and `Processing` are included because the library computes derived scientific quantities and transforms retrieved index data. `Physics-Based` is not selected: although the airglow calculation implements published physical rate equations, the named wrapped climatologies are principally empirical, making `Empirical` the more precise controlled classification. Plotting is confined to example scripts rather than a public visualization API, and the Dockerfile is a deployment option rather than server/environment functionality, so those categories are not selected.

### 5. Related Region (RECOMMENDED)

**Values:**

- Earth Atmosphere
- Earth Lower and Middle Atmosphere
- Earth Ionosphere
- Earth Thermosphere

The existing HSSI value `Earth Atmosphere` remains the broad physical scope. HWM covers atmospheric winds from the lower atmosphere through the thermosphere, IRI describes ionospheric plasma, and MSIS describes the neutral atmosphere and thermosphere; the more specific flat-region values make those independently supported scopes explicit. `Earth Auroral Subregion` is not selected because airglow is not synonymous with aurora and pyglow is not restricted to auroral locations. `Earth Magnetosphere` is not selected because IGRF supplies an internal geomagnetic field and field-line utility rather than a full magnetospheric model.

### 6. Authors (MANDATORY)

**Author 1:**

- **Name:** Timothy M. Duly
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 2:**

- **Name:** Mark D. Butala
- **Author Identifier:** Not found
- **Affiliation:** Not found

`setup.py` uses the full display name Timothy M. Duly; `License.md` and the PyHC registry use Timothy Duly. These primary project metadata sources and Timothy M. Duly's CEDAR abstract name Timothy alone. The PYSAT paper's bibliography instead credits the software to Duly and Butala, and the pin-bounded history contains substantive Mark Butala contributions. Taken together, the scholarly software citation and substantive contribution history support classifying Mark D. Butala as a software author despite the single-author project metadata. The source tree contains no ORCID or ROR identifier for either author.

A fielded ORCID search for given name Timothy and family name Duly produced one candidate, https://orcid.org/0000-0001-5424-0921. Its public name is Timothy Duly, but its public record exposes no works, affiliations, email, URLs, or alternate names that connect it to this repository. The candidate is therefore not recorded because independent identity linkage is lacking.

Contemporary repository source comments use an `illinois.edu` address, and a publication by Timothy M. Duly identifies the University of Illinois at Urbana-Champaign. The exact institutional ROR is University of Illinois Urbana-Champaign, https://ror.org/047426m28. No affiliation is recorded for Timothy because the repository does not explicitly declare an author affiliation; later employment at Spire Global is not evidence of the affiliation under which pyglow was authored. No affiliation is recorded for Mark D. Butala because the reviewed software-author evidence does not establish one in this context.

### 7. Software Name (MANDATORY)

**Value:** pyglow

The lower-case name is used by `setup.py`, the repository, the package import, the wiki, the PyHC registry, and the existing HSSI record. The capitalized PyGlow name on PyPI belongs to an unrelated project.

### 8. Description (MANDATORY)

**Value:** pyglow is a Python module that wraps several upper atmosphere climatological models written in FORTRAN, such as the Horizontal Wind Model (HWM), the International Geomagnetic Reference Field (IGRF), the International Reference Ionosphere (IRI), and the Mass Spectrometer and Incoherent Scatter Radar (MSIS). It includes HWM 1993/2007/2014, IGRF 11/12, IRI 2012/2016, and MSIS 2000. pyglow offers access to these models and geophysical indices (AP, Kp, F10.7, DST, AE) in a convenient, high-level object-oriented interface within Python.

This wording is retained from the existing HSSI record because it accurately and specifically summarizes `README.md` lines 11-31 at the pinned revision.

### 9. Concise Description (OPTIONAL)

**Value:** Upper atmosphere climatological models in Python

This exact phrase is the GitHub repository description, the tagline displayed in the project logo, and the title of the CEDAR 2014 abstract.

### 10. Publication Date (RECOMMENDED)

**Value:** 2013-08-09

GitHub records repository creation on 2013-08-09. The first git commit followed on 2013-08-10, so the existing publication date remains the earliest authoritative public-project date.

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

No formal software publication record was found. GitHub is retained as publisher because it is the public host and distribution point for the software and its wiki.

### 12. Version (RECOMMENDED)

- **Version Number:** 2.2
- **Version Date:** 2019-01-11
- **Version Description:** Docker for pyglow (#81)
- **Version PID:** Not found

At the pinned revision, `src/pyglow/constants.py` declares `VERSION = '2.2'`, and `src/pyglow/__init__.py` exposes that value as `__version__`. Commit `e8a0e85219c9da9b3464dc9469b04c1e650cc53c` changed the constant from 2.1 to 2.2 on 2019-01-11 with the description recorded above. Earlier commits explicitly added `pyglow-0.21.tar.gz` and `pyglow-0.21.zip` distributions, confirming that the project used intentional version numbers despite having no current git tags or GitHub Releases.

Before this refresh, the HSSI version attachment had an empty number and therefore did not communicate the source-defined version. GitHub's repository `updated_at` value is not a version date, and the unrelated PyPI package's 0.1.7 must not be used. No version-specific persistent identifier was found.

### 13. Programming Language (RECOMMENDED)

**Values:**

- Fortran77
- Fortran90
- Python 3.x

The consistent criterion is languages central to the shipped user-facing Python interface and to the bundled or wrapped model implementations, rather than every language mentioned in comments or historical lineage. Python 3 is the public interface and installation target; fixed-form and free-form Fortran implement the wrapped models and are compiled through f2py. There is no shipped IDL, MATLAB, or Julia implementation. MATLAB appears only as code-lineage and comparison context, while the source does not identify distinct Fortran 2003 or Fortran 2008 implementations. The three existing HSSI values therefore remain the complete important-language set.

### 14. Reference Publication (OPTIONAL)

**Value:** Not found

The repository and wiki do not designate a DOI-bearing paper as the preferred publication describing pyglow. Timothy M. Duly's CEDAR 2014 abstract directly presents the package, but it has no DOI and cannot populate this DOI-only field. DOIs embedded in bundled model files describe the upstream HWM, IRI, and index products rather than pyglow itself.

### 15. License (RECOMMENDED)

- **License:** MIT License

`License.md` contains the MIT License text and names Timothy Duly as copyright holder. `MIT License` is the exact closed-vocabulary row. The license URI belongs to that shared controlled row and is not a separate per-software value.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:**

- airglow
- climatological models
- electron density
- f10.7
- geomagnetic field
- geophysical indices
- hwm
- igrf
- ionosphere
- ionosphere thermosphere mesosphere
- iri
- mesosphere
- msis
- neutral atmosphere
- thermosphere
- upper atmosphere

The exact lower-case spellings reuse existing keyword rows; title-cased display variants must not create duplicates. Nine established keywords are retained. `ionosphere`, `thermosphere`, `mesosphere`, `geomagnetic field`, `neutral atmosphere`, `electron density`, and `f10.7` add separately searchable scientific concepts directly exposed by the wrapped models and index interface. `specific` came from the PyHC registry taxonomy but is omitted because it has no clear standalone scientific meaning. The compound PyHC keyword remains separately useful because it preserves the registry's established concept.

### 17. Data Sources (OPTIONAL)

**Values:**

- GFZ
- HTTP/HTTPS Directories
- WDC

`src/pyglow/indice_maintenance.py` retrieves Kp/AP/F10.7 data from GFZ and Dst/AE data from World Data Center Kyoto over HTTP or HTTPS. These three controlled values represent the authored remote sources and transport directly. `Other` is omitted because it is redundant once those sources are represented specifically.

### 18. Input File Formats (RECOMMENDED)

**Value:** ascii

The index stores and bundled model data use plain-text ASCII formats, including fixed-width index files, model coefficient files, and Fortran-readable data. `ascii` is the exact existing controlled value.

### 19. Output File Formats (RECOMMENDED)

**Value:** Not found

The pyglow package returns model results through Python objects and arrays. The public API does not designate or write an output file format, so formats that users could choose through general Python I/O are deliberately not inferred.

### 20. Operating System (RECOMMENDED)

**Values:**

- Linux
- Mac

The README provides native Linux installation commands, a Mac installation-path example, and a Linux Docker build. No Windows installation, continuous-integration, or support evidence appears at the pinned revision. The two existing values are therefore retained without inferring Windows or a generic OS-independent value.

### 21. CPU Architecture (RECOMMENDED)

**Value:** CPU Independent

The Python and portable Fortran sources have no GPU, accelerator, or architecture-specific requirement. Compilation is required, but no CPU family is prescribed, so the existing controlled value remains appropriate.

### 22. Related Phenomena (OPTIONAL)

**Value:** Not found

Of the available controlled phenomena, `Geomagnetic Storms` is plausibly related because pyglow exposes Dst, AE, Kp/AP, and HWM disturbance-wind behavior. It is nevertheless omitted because the package is a general climatological-model and index interface rather than storm-specific software; none of the solar-only phenomena applies.

### 23. Development Status (RECOMMENDED)

**Value:** Inactive

The repository is not archived, but its last source commit was 2023-05-02 and the pinned README states that pyglow was already far behind on maintenance and difficult to install in April 2023. The exact controlled definition of `Inactive` is: “The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows.” This fits the available evidence. `Unsupported` would require evidence that the authors had ceased all work and a new maintainer may be desired; the repository does not make that stronger claim. GitHub's `updated_at` timestamp is not commit activity.

### 24. Documentation (RECOMMENDED)

**Value:** https://github.com/timduly4/pyglow/wiki

The README links this separate GitHub wiki, and the existing HSSI record uses it. The wiki exists at its own repository revision and currently contains acknowledgement guidance; the README remains the more extensive installation and API overview, but the established documentation URL is valid.

### 25. Funder (OPTIONAL)

**Value:** Not found

No repository, archive, wiki, registry, DOI record, or author-keyed source attributes funding for pyglow itself. Funding attached to papers that merely use pyglow is not software funding.

### 26. Award Title (OPTIONAL)

**Value:** Not found

No award or grant title is attributed to pyglow by the repository, wiki, registry, or related metadata sources.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values:**

- https://cedarscience.org/2014-it-poster-list
- https://doi.org/10.1029/2018JA025297
- https://doi.org/10.1029/2020JA027972
- https://doi.org/10.1029/2018JA025877

The CEDAR 2014 meeting record is Timothy M. Duly's direct abstract presenting pyglow as a common Python framework for HWM, IGRF, IRI, and MSIS; its stable meeting page is used because the abstract has no DOI. The PYSAT paper, https://doi.org/10.1029/2018JA025297, cites and describes pyglow. Pysat release notes separately document coupled satellite/model simulation using pyglow and Python 3 pyglow integration, supporting both scientific use and interoperability. Mesquita et al. 2020, https://doi.org/10.1029/2020JA027972, used an archived `pyglow-master.zip` to generate empirical-model results, as documented by its associated Zenodo dataset record. https://doi.org/10.1029/2018JA025877 has a dedicated pyglow subsection describing its wrapped models and index downloads and independently describes pysat's use of pyglow for model access. Other papers found in literature searches cite pyglow or use one wrapped model but lack evidence that the developer prioritized them, so they are not selected.

### 28. Related Datasets (OPTIONAL)

**Value:** https://doi.org/10.5880/Kp.0001

The Kp/AP/F10.7 input file distributed with pyglow identifies this GFZ DOI for the Kp index series, and the update code retrieves the same source product. Dst and AE are retrieved from WDC Kyoto but the source does not identify dataset DOIs for them. The Mesquita Zenodo dataset includes a copy of pyglow and uses it to produce results; it is not a dataset that pyglow is designed to support and is therefore recorded through its paper in Field 27 rather than here.

### 29. Related Software (OPTIONAL)

**Values:**

- https://github.com/space-physics/hwm93
- https://github.com/space-physics/msise00
- https://github.com/space-physics/igrf
- https://github.com/rilma/pyIRI2016
- https://github.com/space-physics/NCAR-GLOW

HWM-93 and MSISE-00 represent model families directly wrapped by pyglow; the HSSI MSISE-00 record also links back to pyglow. IGRF-13 and pyIRI2016 are closely corresponding repository-backed Python interfaces for two other wrapped model families. GLOW is a distinguishing alternative for upper-atmosphere and airglow calculations. These URLs are the exact code-repository identities stored for the corresponding HSSI entries.

IRI-90 and IGRF-14 were considered but are redundant generation alternatives once the closer repository-backed IRI and IGRF family candidates are represented. Generic Python dependencies and build tools are excluded because they do not distinguish pyglow.

### 30. Interoperable Software (OPTIONAL)

**Value:** https://github.com/pysat/pysat

Pysat release metadata documents pyglow integration for Python 3 and a coupled satellite/model simulation that uses pyglow; pysatMissions also exposed pyglow access methods for pysat Instrument objects. This is a demonstrated domain-tool integration, and the URL is the exact code repository stored for pysat in HSSI.

Numpy, SciPy, pandas, matplotlib, python-dateutil, future, pytest, compilers, Docker, and Jupyter are deliberately excluded. Dependency, build, plotting-example, or shared-runtime presence does not establish peer-tool data exchange under the Field 30 relevance rule.

### 31. Related Instruments (OPTIONAL)

**Value:** Not found

The pyglow package is an instrument-agnostic climatological-model wrapper and index interface. UARS, WINDII, and HRDI appear only in embedded HWM07 metadata as observations used to construct that upstream model; pyglow does not read or process their measurements. “Mass Spectrometer and Incoherent Scatter Radar” expands the MSIS model name rather than identifying particular supported instruments. These mentions fail the designed-to-support relevance gate before vocabulary resolution, so no instrument name or identifier is emitted.

### 32. Related Observatories (OPTIONAL)

**Value:** Not found

No observatory or mission is designed into pyglow's input, output, or API. The README's ISS mention only credits the photograph used in the logo, and the UARS mention belongs to upstream HWM model-generation history. A user searching for those observatories' data would not reasonably expect this general model wrapper as a result, so no observatory association is selected.

### 33. Logo (OPTIONAL)

**Value:** https://raw.githubusercontent.com/timduly4/pyglow/1988757f3b6a4bd5ed98266a3fb1dc64f2513fc5/logo.png

This revision-pinned URL returns a valid PNG byte-identical to the repository's `logo.png`. Visual inspection shows the `pyglow` name and “upper atmosphere climatological models in Python” tagline over the airglow photograph displayed at the top of the README. The existing HSSI value is therefore retained without substituting a different graphic.
