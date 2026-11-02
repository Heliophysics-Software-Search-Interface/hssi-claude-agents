# HSSI Metadata Extraction Results

**HSSI Software ID:** aebd4757-08dc-4ca0-be33-aa85171de59d
**Repository:** https://github.com/JHUAPL/kaiju
**Source Revision:** 9e19bfc61a63206e7e74340b5dbf0b7537afa8a7
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-11-02
**Validation Status:** PASS

**Release note — MAGE_1.5.0.** The Source Revision above is the `MAGE_1.25.1` release commit. At the
MAGE_1.5.0 release update (2026-11-01) the fields that release could have changed were re-read at the
`MAGE_1.5.0` tag, commit `ec8b1b3816ecf8b3ebedced8d1947d94f288497d`, which is an ancestor of `master`;
`master` (`220b76f6772c1ed6937b951da2e0d782cb596f10`) differs from the tag only in the README's citation
list, reordered newest first with the MAGE_1.5.0 version DOI added. Sections rewritten at that update name
the revision their evidence was read at; a citation that names no revision was read at the Source
Revision. The `master` commit `3382b1f2fd39419e5a43d4c7bc5427029d48291a` (2026-08-24, "Update README.md")
that earlier versions of Fields 22 and 33 cited is no longer on any branch or tag of the upstream
repository: `master` was rewritten without it.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.16818620

*Source: CITATION.cff line 6, DataCite concept DOI metadata, and the Zenodo concept record. This is the all-versions concept DOI; the latest version DOI is recorded in Field 12.*

*Re-checked at MAGE_1.5.0: unchanged. The README at `ec8b1b38` now shows this DOI in its badge and asks for it as the "MAGE software, all versions" citation (`README.md:3, 79`), and the concept DOI resolves to the MAGE_1.5.0 deposit.*

### 3. Code Repository (MANDATORY)
https://github.com/JHUAPL/kaiju

*Source: git remote origin, CITATION.cff line 7, and docs/source/building/index.rst lines 27-32.*

### 4. Software Functionality (RECOMMENDED)
- Coordinate Transforms
- Coordinate Transforms:Heliospheric
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Models and Simulations
- Models and Simulations:Data Guided
- Models and Simulations:Empirical
- Models and Simulations:First Principles
- Models and Simulations:Forecasting
- Models and Simulations:MHD
- Models and Simulations:Physics-Based
- Servers and Environments
- Servers and Environments:High Performance Computing
- Servers and Environments:Software or Environment Container

*Source: README.md lines 5-25 identify MAGE, GAMERA-helio, GAMERA, RAIJU, Dragon King, REMIX, and TIEGCM. CMakeLists.txt lines 122-274 builds CHIMP, GAMERA, Dragon King, REMIX, RAIJU, VOLTRON, GAMERA-helio, and MPI variants. Coordinate transforms are supported by src/base/kai2geo.F90 and src/base/defs/mixdefs.F90 for SM/GEO/GSM/APEX transforms and by src/chimp/gridloc.F90 for LFM and heliospheric spherical coordinates. Data access/retrieval and file conversion are supported by docs/source/running/geoGRQuickStart.rst lines 76-107 and scripts/makeitso/makeitso.py lines 848-855 for CDAWeb solar-wind retrieval and HDF5 conversion; docs/source/running/helioQuickStart.rst lines 54-87 and scripts/makeitso-gamhelio/makeitso-gamhelio.py lines 227-256 support WSA FITS input. Field-line tracing and analysis tools are built in CMakeLists.txt lines 130-143 and documented in docs/source/tools. 2D slice extraction is documented in docs/source/tools/slice.rst, and particle distribution/PSD processing is implemented in src/chimp/psdio.F90. RAIJU moments and precipitation outputs are in src/raiju/raijuIO.F90. Container and HPC support are documented in docs/source/building/index.rst lines 17-48 and containers/containerization.md lines 95-168, 220-228. Standalone visualization, mission-operations support, and observatory/instrument model categories were considered but not selected because visualization is delegated to companion Kaipy/quicklook workflows, CCMC/HPC packaging does not make the software mission-specific, and WSA/TIEGCM coupling does not establish instrument or observatory model support.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`); no value added or removed. The release adds MAGE coupled with the WACCM-X whole-atmosphere model, the "GRX" configuration (`src/voltron/mpi/modelInterfaces/gcmCouple_mpi.F90`, `docs/source/running/geoGRXQuickStart.rst`); the `engage.py` run-preparation front end for the GR, GRT and GRX configurations (`scripts/engage/engage.py:153`); and `scripts/waxrun/`, which creates and builds the WACCM-X cases and generates their nudging files by regridding and vertically interpolating MERRA2 meteorology onto the WACCM-X grid (`scripts/waxrun/nudge_gen.py:3-20`). The stored `Models and Simulations` children, `Data Processing and Analysis: Processing` and `Servers and Environments: High Performance Computing` already cover these. `Data Processing and Analysis: Data Assimilation` was considered for the nudging and rejected: WACCM-X performs the nudging at run time through CAM's `Nudge_*` settings (`scripts/waxrun/config/user_nl_cam.coupled.j2:93-95`), Kaiju only prepares its input files, and `Models and Simulations: Data Guided` already records that runs are driven by data. No stored capability was removed: TIEGCM coupling moved from `src/remix/tgcm.F90` and `src/voltron/mpi/gcm_mpi.F90` (both deleted) into `gcmCouple_mpi.F90`, and run preparation still fetches the CDAWeb solar-wind boundary data through `cda2wind` (`scripts/makeitso/makeitso.py:2128-2137`).*

### 5. Related Region (RECOMMENDED)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres
- Solar Environment
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Thermosphere
- Earth Magnetotail
- Earth Auroral Subregion
- Solar Wind
- Jupiter Magnetosphere
- Saturn Magnetosphere
- Earth Lower and Middle Atmosphere

*Source: README.md lines 5-25 and docs/source/index.rst lines 4-11 describe geospace, inner heliosphere, planetary magnetospheres, solar wind, ionosphere, and thermosphere support.*

*Source for `Earth Inner Magnetosphere`: `README.md:18-20` identifies RAIJU as the inner-magnetosphere model, corroborated by `src/voltron/innermagsphere.F90:1` and `src/base/imaghelper.F90:1`.*

*Source for `Earth Ionosphere`: `README.md:22-25` identifies the REMIX ionospheric-electrodynamics module and TIEGCM ionosphere-thermosphere model; `src/raiju/raijuGrids.F90:352` explicitly maps onto a spherical grid in the ionosphere.*

*Source for `Earth Thermosphere`: `README.md:24-25` identifies the TIEGCM ionosphere-thermosphere model, and `docs/source/building/buildAitken_GTR.rst:119` describes the coupled thermosphere and ionosphere system.*

*Source for `Earth Magnetotail`: `docs/source/tools/slice.rst:140-142` and `docs/source/tools/chop.rst:138-140` document the `xTail` option as including magnetotail cells in the model domain.*

*Source for `Earth Auroral Subregion`: `src/dragonking/auroralhelper.F90:1` identifies auroral-conductance routines, while `src/remix/mixconductance.F90:49,180` describes auroral precipitation and conductance and implements `conductance_aurora`.*

*Source for `Solar Wind`: `README.md:8-9` identifies solar-wind simulation as a supported environment, and `src/gamera/apps/wind.F90:1` identifies utilities for solar-wind boundary conditions.*

*Source for `Jupiter Magnetosphere`: `src/base/planethelper.F90:55-60` defines Jupiter-specific planetary and magnetospheric parameters used by the magnetosphere setup in `src/gamera/apps/msphutils.F90:80-82`.*

*Source for `Saturn Magnetosphere`: `src/base/planethelper.F90:48-54` defines Saturn-specific planetary and magnetospheric parameters; `docs/source/_obsolete/magnetosphere/exoOuterPlanets/exoOuterPlanets.rst:4,59` documents non-Earth planetary-magnetosphere runs and names Saturn among the planets with defined parameters.*

*Source for `Earth Lower and Middle Atmosphere` (added at MAGE_1.5.0, read at `ec8b1b38`): `README.md:16-27` names the WACCM-X model among the components MAGE 1.5 includes, a "whole-atmosphere model, from the Earth's surface to the upper thermosphere." In this GRX configuration Kaiju couples to WACCM-X (`src/voltron/mpi/modelInterfaces/gcmCouple_mpi.F90:369-375`), and its own `scripts/waxrun/nudge_gen.py` processes lower- and middle-atmosphere meteorology, MERRA2 winds, temperature, surface pressure and humidity on the 72 MERRA2 levels, onto the WACCM-X grid (`nudge_gen.py:9-20`). Its coarse row, `Earth Atmosphere`, was already recorded.*

### 6. Authors (MANDATORY)
- **Author:** Slava Merkin
  - **Author Identifier:** https://orcid.org/0000-0003-4344-5424
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Harry Arnold
  - **Author Identifier:** https://orcid.org/0000-0002-0449-1498
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Shanshan Bao
  - **Author Identifier:** https://orcid.org/0000-0002-5209-3988
  - **Affiliation:**
    - **Organization:** Rice University
      - **Affiliation Identifier:** https://ror.org/008zs3103
- **Author:** Jeffrey Garretson
  - **Author Identifier:** https://orcid.org/0000-0003-3805-9860
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Dong Lin
  - **Author Identifier:** https://orcid.org/0000-0003-2894-6677
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
    - **Organization:** Clemson University
      - **Affiliation Identifier:** https://ror.org/037s24f05
- **Author:** John Lyon
  - **Author Identifier:** https://orcid.org/0000-0002-5759-9849
  - **Affiliation:**
    - **Organization:** Gamera Consulting
- **Author:** Andrew McCubbin
  - **Author Identifier:** https://orcid.org/0000-0002-6222-3627
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Adam Michael
  - **Author Identifier:** https://orcid.org/0000-0003-2227-1242
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Kevin H. Pham
  - **Author Identifier:** https://orcid.org/0000-0001-5031-5519
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Elena Provornikova
  - **Author Identifier:** https://orcid.org/0000-0001-8875-7478
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Nikhil Rao
  - **Author Identifier:** https://orcid.org/0000-0003-2639-9892
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Anthony Sciola
  - **Author Identifier:** https://orcid.org/0000-0002-9752-9618
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Kareem Sorathia
  - **Author Identifier:** https://orcid.org/0000-0002-6011-5470
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Frank Toffoletto
  - **Author Identifier:** https://orcid.org/0000-0001-7789-2615
  - **Affiliation:**
    - **Organization:** Rice University
      - **Affiliation Identifier:** https://ror.org/008zs3103
- **Author:** Aleksandr Ukhorskiy
  - **Author Identifier:** https://orcid.org/0000-0002-3326-4024
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Wenbin Wang
  - **Author Identifier:** https://orcid.org/0000-0002-6287-4542
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Michael J. Wiltberger
  - **Author Identifier:** https://orcid.org/0000-0002-4844-3148
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Eric Winter
  - **Author Identifier:** https://orcid.org/0000-0001-5226-2107
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Haonan Wu
  - **Author Identifier:** https://orcid.org/0000-0002-3272-8106
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874
- **Author:** Jordi Vila-Pérez
  - **Author Identifier:** https://orcid.org/0000-0003-3164-0863
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
    - **Organization:** NSF NCAR High Altitude Observatory
      - **Affiliation Identifier:** https://ror.org/03773p874

*Source: An earlier HSSI record contained only three incomplete author entries. The complete creator set comes from CITATION.cff lines 10-86 and DataCite/Zenodo metadata. Through MAGE_1.25.1, CITATION.cff and the Zenodo deposits spelled two given names "Haonon" (Wu) and "Jeffery" (Garretson); the ORCID records give "Haonan" and "Jeffrey", and the project corrected both in CITATION.cff before MAGE_1.5.0 (commit `fb71fc3c`, "Fixing typos in people's names.", 2026-10-09), as the MAGE_1.5.0 Zenodo deposit also does. ROR identifiers for JHU/APL, NSF NCAR, and Rice University come from ROR; no ROR was found for Gamera Consulting.*

*The names and affiliations above are the ones HSSI stores on these Person records, which are shared with other catalogue entries. HSSI stores "Kevin H." Pham and "Michael J." Wiltberger where CITATION.cff and their ORCID records write "Kevin" and "Michael"; a middle initial is a style variant, and the README's citation list writes "Pham, K. H." and "Wiltberger, M. J.", so the stored forms are kept (Field 6 rule 10). The records of the NSF NCAR authors (Lin, Pham, Rao, Wang, Wiltberger, Wu and Vila-Pérez) also carry NSF NCAR High Altitude Observatory beside NSF National Center for Atmospheric Research (Vila-Pérez's record carried HAO alone before MAGE_1.5.0); HAO is the NCAR laboratory they work in, and stored affiliations are kept (rule 17). Earlier versions of this list showed only the CITATION.cff forms for these authors.*

*Garretson's given name is "Jeffrey". CITATION.cff and the Zenodo deposits spelled it "Jeffery" through MAGE_1.25.1, and HSSI held that spelling until the MAGE_1.5.0 release update. The project has since corrected it as a typo (commit `fb71fc3c`, an ancestor of the MAGE_1.5.0 tag), and "Jeffrey" is also the given name on his ORCID record and in his commit address (`Jeffrey.Garretson@jhuapl.edu`), so the stored spelling matched no current source and was corrected (Field 6 rule 11). The two spellings differ by a word, so the correction renamed his Person record, and the new spelling shows on every entry that record serves: Kaiju and Kaipy, both of which credit him with ORCID 0000-0003-3805-9860. No other Person record held the name "Jeffrey Garretson". Kaipy's own CITATION.cff still writes "Jeffery"; that is the same typo, not a source for keeping it.*

*Changes at MAGE_1.5.0 (read at `ec8b1b38` and in the MAGE_1.5.0 Zenodo deposit, https://doi.org/10.5281/zenodo.23271204):*

- *Jordi Vila-Pérez is added (rule 8). The MAGE_1.5.0 Zenodo deposit lists "Vila Perez, Jordi" as its twentieth creator, with ORCID 0000-0003-3164-0863 and affiliation NSF National Center for Atmospheric Research, although CITATION.cff at the tag still lists the 19 authors above; he is also a committer in the release range (`jvilaperez <jvilap@ucar.edu>`, Dragon King and REMIX coupling work). HSSI already holds a Person record carrying that ORCID, spelled "Jordi" / "Vila-Pérez" as on his ORCID record, which serves the TIEGCM v3.0 entry, so this entry uses that record under its stored spelling; the deposit's "Vila Perez" is the same name written without the accent and hyphen (rule 10). NSF National Center for Atmospheric Research (https://ror.org/05cvfcr44) comes from the deposit (rule 21) and joins the NSF NCAR High Altitude Observatory affiliation the record already carried, which matches his ORCID employment (University Corporation for Atmospheric Research, "National Center for Atmospheric Research, High Altitude Observatory", from 2024-09-03). He is listed last, as in the deposit (rule 29).*
- *Dong Lin's affiliation in the MAGE_1.5.0 deposit is Clemson University, while CITATION.cff at the tag still gives NSF National Center for Atmospheric Research. His ORCID employment record dates the two rather than contradicting them: University Corporation for Atmospheric Research, High Altitude Observatory, from 2019-06 to 2025-08, then Clemson University (Physics and Astronomy, Assistant Professor) from 2025-08, disambiguated to https://ror.org/037s24f05. His commits in the release range, from 2026-07 and 2026-08, fall in the Clemson period, and CITATION.cff was not refreshed for this release (its `version` still reads 1.25.1). Clemson University is therefore added with its ROR (rule 21), and the NCAR affiliations stay (rule 17); those commits were made on NCAR's Derecho system under a ucar.edu address, so the NCAR affiliations are not stale either.*

### 7. Software Name (MANDATORY)
Kaiju

*Source: README.md line 1 and the repository name. CITATION.cff line 3 titles the DOI record as MAGE because MAGE is a primary application within Kaiju.*

### 8. Description (MANDATORY)
Kaiju software includes the Multiscale Atmosphere-Geospace Environment (MAGE) model developed by the Center for Geospace Storms (CGS) as well as other scientific software for simulation of heliospheric environments such as planetary magnetospheres and the solar wind. Currently supported applications include MAGE (version 1.5) and GAMERA-helio, i.e., the geospace and inner heliosphere applications of the kaiju software. MAGE 1.5 includes GAMERA global magnetosphere model, the RAIJU model of the inner magnetosphere, which is a full rewrite of the Rice Convection Model (RCM), the new energetic precipitation model Dragon King, the REMIX ionospheric electrodynamics module, the TIEGCM model of the ionosphere-thermosphere and the WACCM-X whole-atmosphere model, from the Earth's surface to the upper thermosphere. Kaiju also includes CHIMP analysis tools for field-line tracing, test-particle calculations, slices, and ground/space magnetic perturbation calculations. The software is primarily modern Fortran with Python run-preparation tooling, uses HDF5 and related input conversion workflows, and is built for serial and MPI/OpenMP high-performance computing runs. Users are encouraged to use the companion Kaipy package for analysis and visualization of Kaiju simulations.

*Source: README.md lines 5-53, CMakeLists.txt lines 122-274, docs/source/building/index.rst lines 17-48, and docs/source/running/geoGRQuickStart.rst lines 76-131.*

*Updated at MAGE_1.5.0 (read at `ec8b1b38`): the second and third sentences are the README's "Current version" paragraph (`README.md:16-27`) verbatim, with its markdown links and code formatting removed. HSSI held "Currently supported applications include MAGE (version 1.25) and GAMERA-helio, the geospace and inner heliosphere applications of the Kaiju software. MAGE 1.25 includes the GAMERA global magnetosphere model, RAIJU inner-magnetosphere model, Dragon King energetic-precipitation model, REMIX ionospheric electrodynamics module, and TIEGCM ionosphere-thermosphere coupling." until the MAGE_1.5.0 release update: a paraphrase of the same paragraph as it read for MAGE 1.25, which no longer named the current version and omitted the WACCM-X whole-atmosphere model that MAGE 1.5 adds, so the project's current text was adopted (Field 8 rule 3). The other sentences are unchanged and still hold at the tag: the CHIMP executables are still built (`CMakeLists.txt:115-126`), and `README.md:55-56` still recommends Kaipy for analysis and visualization.*

### 9. Concise Description (OPTIONAL)
HPC space-physics modeling framework for MAGE coupled geospace simulations and GAMERA-helio inner-heliosphere simulations, built around the GAMERA MHD solver.

*Source: Derived from README.md lines 5-25 and docs/source/index.rst lines 4-11.*

*Re-checked at MAGE_1.5.0: still accurate. A preview need not name every MAGE component, so the WACCM-X addition does not make it materially incomplete (Field 9 rule 5).*

### 10. Publication Date (RECOMMENDED)
2025-06-23

*Source: the publication date of the first public release, GitHub release `v1.25` ("Lightning Bolt"), published 2025-06-23T13:38:43Z, whose body begins "This is the first official open-source release of the kaiju software." (Field 10 rule 4). HSSI held 2025-12-12 until the MAGE_1.5.0 release update: the DataCite issued and Zenodo publication date of the MAGE_1.25.1 deposit, the date of a later release (rule 1). The concept DOI's issued date moves with every deposit (2026-10-10 once MAGE_1.5.0 was deposited), so it never dates first publication.*

*Alternatives considered: 2025-06-22, the commit date of the lightweight `v1.25` tag, which has no date of its own and was committed before the release was published; 2025-06-16, the GitHub repository's `created_at` and the HSSI value before 2025-12-12, which does not satisfy the first-public-source anchor because the history long predates it (rule 3); 2025-08-12, the first Zenodo version deposit (MAGE_0.75.5); and the tags older than June 2025 (`kaiju_v1.0.0` of 2022-02-25, the `KAIJU_CCMC_*`, `GAMHELIO_CCMC_*` and `MAGE_CCMC_*` series, and `dev_preOSS` of 2025-06-09), which were cut before the code was open-sourced and so were not public releases. The tag name `dev_preOSS` marks the code's state before open-sourcing, and the v1.25 release calls itself the first official open-source release.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source: DataCite/Zenodo metadata for DOI 10.5281/zenodo.16818620.*

### 12. Version (RECOMMENDED)
- **Version Number:** MAGE_1.5.0
- **Version Date:** 2026-10-09
- **Version Description:** Not found
- **Version PID:** https://doi.org/10.5281/zenodo.23271204

*Source: GitHub release `MAGE_1.5.0` ("MAGE 1.5.0", not a pre-release), published 2026-10-09T22:03:28Z from tag `MAGE_1.5.0` at commit `ec8b1b3816ecf8b3ebedced8d1947d94f288497d`, an ancestor of `master`; DataCite and Zenodo record 23271204 (version "MAGE_1.5.0", `IsSupplementTo` https://github.com/JHUAPL/kaiju/tree/MAGE_1.5.0), the newest version of the concept DOI. The number is written in the tag form, as the earlier MAGE_1.25.1 was.*

*Release order (Field 12 rule 3): MAGE numbers its versions in quarter steps (0.75, 1.0, 1.25, 1.5), so a version-string sort puts 1.5 below 1.25 although it is newer. The order comes from the project's own records: the README at the tag names version 1.5 as current (`README.md:16-17, 30`), the concept DOI's versions run MAGE_0.75.5, MAGE_1.0.5, MAGE_1.25.0, MAGE_1.25.1, MAGE_1.5.0, and the `MAGE_1.5.0` tag is the newest by creation date and has `MAGE_1.25.1` in its history. HSSI held MAGE_1.25.1 (release date 2025-12-12, PID https://doi.org/10.5281/zenodo.17915213) until the MAGE_1.5.0 release update.*

*Release date: the GitHub release's UTC publication day (rule 7). Zenodo gives the deposit a publication date of 2026-10-10 (created 2026-10-09T22:04Z), and CITATION.cff at the tag still declares `version: "1.25.1"` and `date-released: 2025-12-01`, not having been updated for this release; neither overrides the release event (rule 8), and the stale CITATION.cff version does not make 1.25.1 current.*

*Version Description: left empty (rule 16). The release has no title beyond its tag, and its body is "This is the open source release for MAGE version 1.5" followed by the README's "Current version" paragraph, which repeats the package description (Field 8 now carries it) rather than saying what changed. The MAGE_1.25.1 description, "First official open-source release of the Kaiju software; adds CONE geometry type and improves OpenMP thread-safety.", belonged to that release and is not carried forward (rule 10).*

*`master` (`220b76f6`) adds only README changes after the tag, and no release newer than MAGE_1.5.0 exists (GitHub releases and tags, and the Zenodo version list, checked 2026-11-02).*

### 13. Programming Language (RECOMMENDED)
- Fortran90
- Fortran 2008
- Python 3.x
- Other

*Source: GitHub/SoMEF language scan and local extension counts show 215 .F90 files and 27 Python files. CMakeLists.txt line 2 declares Fortran and C, but line 3 states C was added for HDF5 build issues rather than code content, and no .c source files were found. Fortran 2008 is supported by the MPI F08 requirement in cmake/compilers.cmake lines 18-37. Python 3.x is used for run-preparation scripts and documentation tooling; Other covers shell, CMake, Dockerfile, and PBS/job templates.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`): 229 .F90 and 43 Python files. The new run-preparation tools (`scripts/engage/`, `scripts/waxrun/`) are Python; their Jinja2 templates (`.j2`), YAML configuration and patch file fall under Other. No new language row applies.*

### 14. Reference Publication (OPTIONAL)
Not found

*Source: the README asks that papers "be cited dependent on which configuration the `Kaiju` software is being run" (`README.md:70-163` at `ec8b1b38`): for the coupled MAGE model, the component papers plus either the all-versions software DOI (Field 2) or a configuration paper (MAGE 0.75 or MAGE 1.0; for MAGE 1.25 and 1.5 it says "Team is working on the publication."); for the individual components, papers for the GAMERA MHD algorithm, GAMERA magnetosphere, REMIX, RAIJU, Dragon King, TIEGCM and WACCM-X; and two papers for GAMERA-helio. That is a per-component citation list with no single paper for the package, so this field stays empty (Field 14 rule 4) and the listed papers go to Field 27. HSSI held https://doi.org/10.3847/1538-4365/ab3a4c (Zhang et al. 2019, "GAMERA: A Three-dimensional Finite-volume MHD Solver for Non-orthogonal Curvilinear Geometries") until the MAGE_1.5.0 release update. It is the GAMERA solver's paper, first in the component list, rather than a paper for Kaiju as a whole, and it is now listed in Field 27.*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*Source: README.md lines 136-139, CITATION.cff line 8, GitHub/SoMEF license metadata, and LICENSE.md lines 6-19.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- space weather
- MAGE
- geospace modeling
- Kaiju
- GAMERA
- GAMERA-helio
- magnetohydrodynamics
- MHD
- magnetosphere
- ionosphere
- thermosphere
- heliosphere
- solar wind
- planetary magnetospheres
- RAIJU
- REMIX
- TIEGCM
- Dragon King
- CHIMP
- field-line tracing
- high performance computing
- CDAWeb
- HDF5
- WSA
- coronal mass ejections
- waccm-x

*Source: DataCite/CITATION.cff keywords plus README.md lines 5-25, 33-53, 67-133; docs/source/running/geoGRQuickStart.rst lines 76-131; docs/source/running/helioQuickStart.rst lines 54-94.*

*Added at MAGE_1.5.0 (read at `ec8b1b38`): `waccm-x`, an existing keyword row, for the WACCM-X whole-atmosphere model that MAGE 1.5 includes and couples to (`README.md:16-27`, `docs/source/running/geoGRXQuickStart.rst:1-7`), listed like the other MAGE components already here (GAMERA, RAIJU, REMIX, Dragon King, TIEGCM); the project presents it as a component of MAGE rather than a dependency, and a searcher looking for magnetosphere coupling with WACCM-X would type it (Field 16 rule 10). Considered and not added: `whole atmosphere`, which restates Field 5's `Earth Lower and Middle Atmosphere`, and `merra2` or `nudging`, which restate Fields 17 and 28 or name a run-preparation step. The MAGE_1.5.0 Zenodo deposit's keywords (space weather, MAGE, geospace modeling) are already listed. Kaiju has no entry in the PyHC registry (`_data/projects_core.yml`, `_data/projects.yml` and `_data/projects_unevaluated.yml`, read 2026-11-01; only its companion Kaipy is listed), so `pyhc package` does not apply (rule 15).*

### 17. Data Sources (OPTIONAL)
- CDAWeb
- Other

*Source: docs/source/running/geoGRQuickStart.rst lines 76-107 and scripts/makeitso/makeitso.py lines 848-855 fetch solar-wind/f10.7 data through CDAWeb. GAMERA-helio uses WSA FITS boundary-condition files (docs/source/running/helioQuickStart.rst lines 54-87), represented as Other/model-derived source data. Observatory/Mission-specific was considered but not selected because the repository does not establish one specific mission or observatory as a supported target.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`): `Other` also stands for the NCAR MERRA2 Global Atmosphere Forcing Data collection (Field 28), which `scripts/waxrun/nudge_gen.py` reads by default from the archive's directory on NCAR's file system (`nudge_gen.py:71-72`); no DataInput row names that archive. No other source was added.*

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- FITS
- HDF5
- JSON
- netCDF3/4
- Other

*Source: docs/source/running/geoGRQuickStart.rst lines 51-78 and 96-107 require CDF support for CDAWeb-derived solar-wind retrieval and produce HDF5 boundary files; docs/source/running/helioQuickStart.rst lines 54-94 uses WSA FITS input and produces HDF5/XML/JSON run files. scripts/makeitso/makeitso.py and scripts/makeitso-gamhelio/makeitso-gamhelio.py read/write JSON and convert INI to XML. TIEGCM coupling requires netCDF data/modules per docs/source/building/buildAitken_GTR.rst lines 28 and 149-152. Plain text/ascii is used for config/tables and generated OMNI text inputs; Other covers XML/INI/PBS run-control files.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`); no change. `scripts/waxrun/nudge_gen.py` reads MERRA2 netCDF files with `netCDF4` (`nudge_gen.py:61, 72`), a further netCDF3/4 input, and the GRX tools read their saved JSON option files when a run is replayed (`docs/source/running/geoGRXQuickStart.rst:261-271`). The TIEGCM build guides cited above were renamed `buildAitken_GRT.rst` and `buildDerecho_GRT.rst`.*

### 19. Output File Formats (RECOMMENDED)
- ascii
- HDF5
- JSON
- Other

*Source: src/base/ioH5.F90 and module-specific IO files write HDF5 outputs; docs/source/running/geoGRQuickStart.rst lines 121-155 and docs/source/running/helioQuickStart.rst lines 89-115 list generated HDF5, JSON, XML, PBS, PNG, and log files. JSON is included for run-option records. Other covers XML/PBS/log products; PNG quicklook plots are not an allowed HSSI format value.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`); no change. The netCDF files a GRX run produces are written by WACCM-X itself (`docs/source/running/geoGRXQuickStart.rst:301-315`), and the netCDF nudging files that `scripts/waxrun/nudge_gen.py` writes (`nudge_gen.py:13, 1030`) are inputs to the coupled run rather than products a user receives (Field 19 rule 2), so netCDF3/4 is not added; Kaiju's own model output remains HDF5 (`geoGRXQuickStart.rst:276-299`).*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

*Source: docs/source/building/index.rst lines 8-48 emphasizes supercomputer/Linux builds and serial single-machine builds; .readthedocs.yaml lines 3-20 uses Ubuntu; cmake/compilers.cmake lines 165-167 explicitly handles Apple Silicon/macOS. No Windows build is documented.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`); no change. The build guides now cover Derecho and Aitken (the Pleiades guide was removed), GRX runs are supported on Derecho only (`docs/source/running/geoGRXQuickStart.rst:7`), and the Apple Silicon handling is at `cmake/compilers.cmake:164-166`.*

### 21. CPU Architecture (RECOMMENDED)
- Apple Silicon arm64
- HPC or HEC
- x86-64

*Source: docs/source/building/index.rst lines 8-21 and build guides document Aitken/Derecho HPC systems; containers/Dockerfile and containers/gamera.def use Intel oneAPI/x86-64 HPC stacks; .readthedocs.yaml lines 8-13 downloads linux-amd64 git-lfs; cmake/compilers.cmake lines 165-167 handles Apple Silicon arm64.*

*Re-checked at MAGE_1.5.0 (`ec8b1b38`); no change (see Field 20). `containers/Dockerfile` and `containers/gamera.def` are unchanged.*

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Wind

*Source: the README citation list and GAMERA-helio documentation discuss CME modeling — Provornikova et al. 2024, "MHD Modeling of a Geoeffective Interplanetary Coronal Mass Ejection…" (`README.md:154-158` at the MAGE_1.5.0 tag `ec8b1b38`; an earlier version of this note cited README lines 130-136 at `master` commit 3382b1f2, which is no longer in the repository's history), and docs/source/_obsolete/heliosphere/helio-cme.rst documents the embedded Gibson-Low flux-rope CME model. Geomagnetic Storms and Solar Wind are included because MAGE, Kaiju's primary application, is developed by the Center for Geospace Storms (README lines 5-7), the README describes modeling of "planetary magnetospheres and the solar wind" (line 9), and the citation list includes storm-time case studies (Sorathia et al. 2023 dawnside-current-wedge; Pham et al. 2022 August-2005-storm thermospheric response) alongside the geoeffective-ICME study — geomagnetic storms and solar-wind coupling are the central science of the MAGE/GAMERA geospace models, not incidental. An earlier note excluded both values in the belief that they were absent from the HSSI Related Phenomena controlled vocabulary; that belief came from a stale six-value documentation list, and both are in fact controlled rows. Substorms, aurora, and ring current remain excluded correctly — they have no controlled row (the earlier note's claim that all five terms were "recorded as keywords" was also inexact: of the five, only solar wind appears in Field 16, alongside coronal mass ejections).*

*Re-checked at MAGE_1.5.0: the WACCM-X coupling extends the model downward through the atmosphere, but no further Related Phenomena row (Coronal Heating, Solar Corona, Solar Flares, X-ray emission) applies.*

### 23. Development Status (RECOMMENDED)
Active

*Source: the README says the `master` branch "contains bleeding-edge code that is under active development" (`README.md:30-31` at `ec8b1b38`; Field 23 rule 4), and recency agrees (rule 6): the last commit on `master` is `220b76f6` of 2026-10-09, and the newest release is MAGE_1.5.0 of 2026-10-09. The repository is not archived.*

### 24. Documentation (RECOMMENDED)
https://kaiju-docs.readthedocs.io/en/latest/

*Source: README.md lines 45-48 and docs/source/index.rst. This broad documentation landing page supersedes the narrower earlier HSSI rules-of-road URL.*

*Re-checked at MAGE_1.5.0: the page resolves (2026-11-01), and the README at `ec8b1b38` links it in its Docs badge and Documentation section (`README.md:4, 48-51`).*

### 25. Funder (OPTIONAL)
Not found

*Source: No funder entries are present in DataCite/Zenodo metadata, CITATION.cff, README.md, or repository documentation. README.md identifies CGS and NASA CCMC availability, but does not state a specific funder for the software metadata record.*

*Re-checked at MAGE_1.5.0: the MAGE_1.5.0 Zenodo deposit carries no grants, and neither CITATION.cff nor the README at `ec8b1b38` names a funder.*

### 26. Award Title (OPTIONAL)
Not found

*Source: No grant or award title/number is present in DataCite/Zenodo metadata, CITATION.cff, README.md, or repository documentation.*

*Re-checked at MAGE_1.5.0: still none, in the MAGE_1.5.0 Zenodo deposit or in CITATION.cff and the README at `ec8b1b38`.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2020GL088227
- https://doi.org/10.1029/2010JA015461
- https://doi.org/10.1002/9781118704417.ch7
- https://doi.org/10.1029/2023JA031594
- https://doi.org/10.1029/2021JA030071
- https://doi.org/10.3847/1538-4357/ad83b1
- https://doi.org/10.1002/2015JA022200
- https://doi.org/10.3847/1538-4365/ab3a4c
- https://doi.org/10.1029/2025JA034219
- https://doi.org/10.1002/2017MS001232

*Source: the README's citation guidance (`README.md:70-163` at `ec8b1b38`), a per-component and per-configuration list (Field 27 rule 4): the GAMERA MHD algorithm (Zhang et al. 2019, https://doi.org/10.3847/1538-4365/ab3a4c), GAMERA magnetosphere (https://doi.org/10.1029/2020GL088227), REMIX (https://doi.org/10.1029/2010JA015461), TIEGCM (Wu et al. 2025, "The NCAR-TIEGCM Version 3.0", https://doi.org/10.1029/2025JA034219), WACCM-X (Liu et al. 2018, "Development and Validation of the Whole Atmosphere Community Climate Model With Thermosphere and Ionosphere Extension (WACCM‐X 2.0)", https://doi.org/10.1002/2017MS001232), the MAGE 0.75 and MAGE 1.0 configuration papers (https://doi.org/10.1029/2023JA031594, https://doi.org/10.1029/2021JA030071), and GAMERA-helio (https://doi.org/10.3847/1538-4357/ad83b1, https://doi.org/10.1002/2015JA022200). Until the MAGE_1.5.0 release update the GAMERA MHD paper was Field 14; it moved here when Field 14 was left empty under that field's rule 4. The TIEGCM and WACCM-X papers were added at that update, after the README added a WACCM-X citation and replaced its TIEGCM citation.*

*Judged as a whole list (rule 4): nine papers the project asks users to cite, each describing one component or configuration a visitor needs in order to understand MAGE: the MHD solver, the magnetosphere, the ionospheric coupler, the ionosphere-thermosphere and whole-atmosphere models, the two published MAGE configurations and the inner-heliosphere application. The list is the project's own citation guide and short enough to scan, so all of it is listed.*

*Kept as an incumbent (rule 7): https://doi.org/10.1002/9781118704417.ch7 (Qian et al. 2014, "The NCAR TIE‐GCM"), the README's TIEGCM citation through MAGE_1.25.1. It describes TIEGCM, a MAGE component; the README at MAGE_1.5.0 cites Wu et al. 2025 for TIEGCM instead.*

*Weighed and not listed:*

- `2025AGUFMSM51B.114S`: Sciola et al., "Connecting stormtime SAR arc variability to mesoscale ring current-plasmasphere evolution via global geospace modeling", AGU Fall Meeting 2025, the README's RAIJU citation. A meeting abstract, never eligible (rule 1).
- `2025AGUFMSA51C1132L`: Lin et al., "Characterizing auroral precipitation and energy deposition with the Dragon King model in MAGE", AGU Fall Meeting 2025, the README's first Dragon King citation. A meeting abstract (rule 1).
- `2022AGUFMSM22F1988B`: Bao et al., "Wave-dependent ring current electron loss and magnetospheric precipitation during a geospace storm", AGU Fall Meeting 2022, the README's second Dragon King citation. A meeting abstract (rule 1).
- `10.5194/egusphere-egu24-4781`: Lin et al., "Characterizing auroral precipitation and ionospheric conductance with the Dragon King model in MAGE", an EGU General Assembly 2024 abstract (rule 1).
- `10.5281/zenodo.16818620` and the version DOIs the README lists beside the MAGE configurations: software deposits, recorded in Fields 2 and 12 (rule 1).

*Crossref, DataCite and Zenodo title searches (2026-11-01) found no deposited poster or paper for any of the four abstracts; a deposited version would be eligible.*

*Use papers (rule 5): MAGE is widely used. An ADS full-text search on 2026-11-01 for the model's name, "Multiscale Atmosphere-Geospace Environment", returned 60 journal articles, 31 of them from 2025 and 2026, and the GAMERA solver paper has more than a hundred citing articles. A list of users would tell a searcher nothing and would bury the component papers, so no use paper is listed. Searches run on 2026-11-01 for publications since this record's extraction (2026-07-24), with a nonsense-token control returning 0: ADS full text for the concept DOI and the five version DOIs and for "JHUAPL/kaiju"; `full:"Multiscale Atmosphere-Geospace Environment"` and `ack:` searches for MAGE, GAMERA and kaiju entered since 2026-07-24. They found no new paper about the software (the README says the MAGE 1.25 and 1.5 papers are still being written), only papers using MAGE, among them:*

- `10.1029/2026GL125752`: Burkholder et al. 2026, a storm-time Kelvin-Helmholtz instability study (rule 5, widely used).
- `10.1029/2026JA035589`: Zhang et al. 2026, ionospheric D-region feedback on the coupled geospace system (rule 5, widely used).
- `10.1029/2026JA035529`: Patel et al. 2026, MHD-test-particle simulations of electrons at GOES 16 and 18 (rule 5, widely used).
- `10.1029/2026JA035392`: Hong et al. 2026, ionospheric conductance during the December 2021 solar eclipse (rule 5, widely used).
- `10.1029/2025EA004941`: Günzkofer et al. 2026, magnetosphere forcing and Joule heating in WACCM-X (rule 5, widely used).
- `10.1029/2025SW004922`: Corti et al. 2026, "Advancing Heliophysics and Space Weather Modeling Through Open Science", which mentions Kaipy only in passing (rule 6).

*Found by the same searches but published before 2026-07-24, and also uses of MAGE or GAMERA-helio, not listed for the same reason:*

- `10.1029/2025AV002071`: Ghag et al. 2026, "Universal Time Influence on Stormtime Magnetosphere Ionosphere Coupling", which cites one of the MAGE software DOIs (rule 5, widely used).
- `10.48550/arXiv.2604.18553`: Gajewski et al. 2026, a preprint on curlometer measurements of field-aligned currents with Swarm, which cites the Kaiju repository (rule 5, widely used).
- `10.3847/1538-4357/ae244f`: Provornikova et al. 2026, GAMERA-helio simulations of coronal mass ejection injection into the inner heliosphere (rule 5, widely used).

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.5065/XVAQ-2X07

*Source (added at MAGE_1.5.0, read at `ec8b1b38`): "MERRA2 Global Atmosphere Forcing Data", dataset d313003 of NCAR's Geoscience Data Exchange (DataCite resource type Dataset; landing page https://gdex.ucar.edu/datasets/d313003/), MERRA2 reanalysis regridded and prepared as meteorological forcing for CESM and WRF. `scripts/waxrun/nudge_gen.py` is a dedicated reader for it: it takes "fields U,V,T,PS,Q from the CESM-prepared MERRA2 f09 archive (RDA d313003, 8 slots/day)" (`nudge_gen.py:9`), by default from the archive's `0.9x1.25` directory with file names `MERRA2_0.9x1.25_{YYYYMMDD}.nc` (`nudge_gen.py:71-72`), to build the nudging files for GRX runs (Field 28 rule 3). The DOI is written in the case the landing page shows.*

*Before MAGE_1.5.0 no dataset DOI or persistent dataset identifier was present in CITATION.cff, DataCite/Zenodo metadata, README.md, or docs. CCMC run availability is a service/model-run access path, not a specific dataset PID. The WACCM-X restart files GRX runs start from (`docs/source/running/geoGRXQuickStart.rst:162-163`) sit in a working directory on NCAR's file system with no identifier or landing page (rule 8).*

### 29. Related Software (OPTIONAL)
- https://github.com/NCAR/tiegcm
- https://github.com/JHUAPL/kaipy
- https://github.com/ESCOMP/CESM

*Source: README.md lines 52-53 and docs/source/python/index.rst lines 9-17 identify kaipy as the companion package for analysis, visualization, and run-preparation dependencies. docs/source/building/buildAitken_GTR.rst lines 115-180 and docs/source/building/buildDerecho_GTR.rst document TIEGCM source/build coupling.*

*At MAGE_1.5.0 (`ec8b1b38`): Kaipy is still the companion package (Field 29 rule 9). The README recommends it "for analysis and visualization of `Kaiju` simulations" (`README.md:55-56`), and the run-preparation scripts rely on it (`docs/source/python/index.rst:4-17`, `docs/source/running/index.rst:8-14`). TIEGCM and WACCM-X are named by the README among the components MAGE 1.5 includes (`README.md:16-27`), domain models whose presence characterises the coupled MAGE configurations GRT and GRX (rule 9). Both are catalogued and are recorded by their entries' stored repository URLs (rule 11): TIEGCM v3.0 as https://github.com/NCAR/tiegcm, and WACCM-X by the CESM entry, https://github.com/ESCOMP/CESM, which describes WACCM-X as a CESM atmosphere configuration and is what a GRX run builds ("Building WACCM-X compiles CESM", `docs/source/running/geoGRXQuickStart.rst:171-172`). The CAM fork and branch that `scripts/waxrun/README.md` clones for the build (`fvitt/CAM`, `waccmx_mage_cplng`) is not recorded, since a build's fork is never the target (rule 12).*

*Kaipy is recorded by its catalogue entry's repository URL, https://github.com/JHUAPL/kaipy, which replaced its concept DOI, https://doi.org/10.5281/zenodo.15801040, at the MAGE_1.5.0 release update (rules 11 and 13): the site shows a related item's raw URL as its link text, and a repository URL is legible where a DOI is not. The concept DOI is still Kaipy's citable identifier, should HSSI ever render resolved titles for related items.*

### 30. Interoperable Software (OPTIONAL)
- https://github.com/NCAR/tiegcm
- https://github.com/JHUAPL/kaipy
- https://github.com/ESCOMP/CESM

*Source: Kaipy is explicitly recommended for analysis and visualization of Kaiju simulations in README.md lines 50-53 and is required for run-preparation/data workflows in docs/source/python/index.rst lines 9-17; DataCite confirms the Kaipy concept DOI. TIEGCM interoperates through coupled GTR workflows and VOLTRON/REMIX interfaces, with build/run requirements documented in docs/source/building/buildAitken_GTR.rst lines 115-180 and code evidence in src/remix/tgcm.F90 / src/voltron/mpi/gcm_mpi.F90. Generic dependencies such as numpy, h5py, netCDF4, matplotlib, SpacePy, and astropy are intentionally excluded.*

*At MAGE_1.5.0 (`ec8b1b38`): Kaiju exchanges fields with TIEGCM and with WACCM-X through Voltron's MPI coupling, a demonstrated exchange with each (Field 30 rule 7). `src/voltron/mpi/modelInterfaces/gcmCouple_mpi.F90` exports to and imports from either model, branching on `isWACCMX` ("MIXCPL Coupling to WACCMX", "MIXCPL Coupling to TIEGCM", lines 369-377), and `src/base/mpi/coupled_layout_mpi.F90:149` places TIEGCM ranks in the coupled MPI layout. The build and run procedures are `docs/source/building/buildDerecho_GRT.rst`, `buildAitken_GRT.rst` and `buildDerecho_GRX.rst` and `docs/source/running/geoGRTQuickStart.rst` and `geoGRXQuickStart.rst`, and `scripts/engage/engage.py` configures the coupled runs (`--component`, `engage.py:153`). The TIEGCM coupling code cited above, `src/remix/tgcm.F90` and `src/voltron/mpi/gcm_mpi.F90`, was removed in favour of these files, and the GTR build guides were renamed GRT. WACCM-X is recorded by the CESM entry's repository URL and Kaipy by its repository URL instead of its concept DOI, as in Field 29.*

*Open leads, not listed: the coupled MPI layout also reserves ranks for "HIDRA_N"/"HIDRA_S" and "SAMI3" (`coupled_layout_mpi.F90:151-173`), but at MAGE_1.5.0 no Kaiju documentation, run tool or exchange routine couples to either, so there is no demonstrated exchange (rule 5). Reconsider if a release documents one.*

### 31. Related Instruments (OPTIONAL)
Not found

*Source: The software is a model/run framework and preprocessing workflow, not a package designed to support a specific instrument's data. WSA FITS, CDAWeb/OMNI, TIEGCM, and GONG-like magnetogram sources were considered but do not establish a specific instrument-level support target under the HSSI relevance gate.*

*Re-checked at MAGE_1.5.0: no instrument-specific support was added. MERRA2 (Field 28) is a reanalysis product, not an instrument.*

### 32. Related Observatories (OPTIONAL)
Not found

*Source: The software supports geospace/heliosphere models and generic data-source workflows, but the repository does not show design support for one specific mission/observatory. OMNI and GONG vocabulary matches were considered; OMNI is a multi-source data product/source and GONG is only an upstream WSA magnetogram source, so neither is listed as a related observatory.*

*Re-checked at MAGE_1.5.0: no mission- or observatory-specific support was added.*

### 33. Logo (OPTIONAL)
https://media.githubusercontent.com/media/JHUAPL/kaiju/ec8b1b3816ecf8b3ebedced8d1947d94f288497d/docs/source/_static/MAGE_Logo_final_dark-bg_vertical.png

*Source: `docs/source/conf.py:38` (at the MAGE_1.5.0 tag `ec8b1b38`) designates docs/source/_static/MAGE_Logo_final_dark-bg_vertical.png (the MAGE logo, 1168x1444 PNG) as the documentation logo. The repository stores the file as a Git LFS pointer (since commit a3db44a6, "Store PNG images in Git LFS", 2025-12-03), so the media.githubusercontent.com endpoint is used because it resolves the LFS object to the actual image (128,262 bytes, sha256 c310f5cecfa73d4fd73d51a2d8a787863d9641132721ddf59d669baaa1bae25c, byte-identical to the pre-LFS blob added in commit ed2428f5). The URL is pinned to the MAGE_1.5.0 release commit, which is tagged and in `master`'s history, so later moves or renames of the file on `master` do not affect it, and its responses permit cross-origin image embedding.*

*Superseded values: https://media.githubusercontent.com/media/JHUAPL/kaiju/3382b1f2fd39419e5a43d4c7bc5427029d48291a/docs/source/_static/MAGE_Logo_final_dark-bg_vertical.png, which HSSI held until the MAGE_1.5.0 release update, served the same image, but its commit, a 2026-08-24 web edit of README.md on `master`, is no longer on any branch or tag of the upstream repository because `master` was rewritten without it; a commit no branch or tag holds is not guaranteed to stay retrievable, so the pin moved to a tagged commit holding the same file (Field 33 rules 1 and 7). Before that, https://raw.githubusercontent.com/JHUAPL/kaiju/master/docs/source/_static/MAGE_Logo_final_dark-bg_vertical.png: after the 2025-12-03 LFS conversion, raw.githubusercontent.com serves that path as the 131-byte LFS pointer text (text/plain), which browsers render as a broken image; it was already broken at the 2026-07-24 extraction. Re-evaluate this field if the MAGE_1.5.0 tag is removed, if the project stops tracking the logo in LFS (a plain raw URL would then suffice), or if conf.py designates a different logo. The ReadTheDocs copy at https://kaiju-docs.readthedocs.io/en/latest/_static/MAGE_Logo_final_dark-bg_vertical.png serves a recompressed rendition of the same image and is the fallback if the media endpoint becomes unavailable.*
