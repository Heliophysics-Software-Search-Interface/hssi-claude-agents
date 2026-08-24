# HSSI Metadata Extraction Results

**HSSI Software ID:** b8495e18-9a18-4e8f-8b88-85db6e74ec22
**Repository:** https://spedas.org/downloads
**Source Revision:** Not applicable — SPEDAS has no public authoritative Git repository. The
reproducibility anchor for this dossier is the official release archive instead:
- Archive URL: `https://spedas.org/downloads/spedas_6_1.zip`
- Filename: `spedas_6_1.zip` (stable release 6.1)
- Retrieved: 2026-08-12
- Size: 82,463,548 bytes
- SHA-256: `dc84c4c27430dd19114b251e17b9c3a5e8f58d9800f5defab400c46dfcfa3a1c`
- MD5: `2b33001ddc3c517efd2c834184a7aa70`
- HTTP `Last-Modified`: Wed, 12 Jun 2024 20:24:30 GMT

That MD5 equals the checksum Zenodo publishes for the `spedas_6_1.zip` file in the 6.1 deposit
(`md5:2b33001ddc3c517efd2c834184a7aa70`, confirmed via `https://zenodo.org/api/records/15023025`), so
the downloads-page archive and the DOI-citable deposit are the same bytes. The extracted tree is
6,996 files, of which 5,882 are `.pro` IDL sources; its top level is `LICENSE.txt`,
`spedas_version.txt`, `.project`, `external/`, `general/`, `projects/`, `spedas_gui/`.

**Extraction Date:** 2026-08-12
**Validation Date:** 2026-08-23
**Validation Status:** PASS

---

**Scope note — read this before weighing the evidence below.** SPEDAS is a multi-mission framework of
~5,900 IDL routines, so several fields (notably 4, 31 and 32) have a very large *true* extent. Where
a field is bounded rather than exhaustive, the bounding rule is stated explicitly with the field and
the excluded candidates are named, so a later refresh can widen the bound deliberately instead of
rediscovering the same ground. Two further caveats apply throughout:

- Because there is no repository, every code claim below cites a path **inside the hash-verified
  `spedas_6_1.zip` tree**, not a Git blob. Paths are given relative to the archive root.
- SPEDAS is not a PyHC package and does not appear in any of the three PyHC registries
  (`projects_core.yml`, `projects.yml`, `projects_unevaluated.yml`, all read in full on 2026-08-12).
  Only **pySPEDAS** — separate software with its own HSSI record — is listed there, as a PyHC Core
  package. PyHC is a Python-package registry, so an IDL framework's absence is expected and is not
  evidence of anything about SPEDAS's standing.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The submitter fields are not part of the stored HSSI record; they are placeholders here.

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.14919975`

Carried over from the existing HSSI record and confirmed correct. This is the Zenodo **concept**
(all-versions) DOI, which is what the project itself instructs users to cite for the software as a
whole: the SPEDAS wiki `Main_Page` says under "Citing SPEDAS" — *"You can cite all versions by using
the DOI 10.5281/zenodo.14919975. This DOI represents all versions, and will always resolve to the
latest one."* DataCite confirms the record exists and carries `HasVersion` relations to twelve
version DOIs (verified against `https://api.datacite.org/dois/10.5281/zenodo.14919975`: the
`relatedIdentifiers` array holds one `IsDescribedBy`, one `IsSupplementTo` and twelve `HasVersion`
entries, spanning versions 1.0, 2.00, 2.1, 3.00, 3.1, 3.2, 3.3, 4.0, 4.1, 5.0, 6.0 and 6.1).
Zenodo agrees from the other direction: the 6.1 record's `metadata.relations.version[0].index` is 11
on a zero-based count, i.e. twelve versions in the concept. Note the off-by-one trap: read as a count
rather than as a zero-based index, that field yields thirteen.

Considered and rejected: the 6.1 **version** DOI `https://doi.org/10.5281/zenodo.15023025`. It is the
right identifier for the *version* (Field 12 records it there), but putting it in Field 2 would pin
the software's identity to one release and contradict the project's own citation guidance.

### 3. Code Repository (MANDATORY)
`https://spedas.org/downloads`

**SPEDAS has no public authoritative Git repository.** `https://spedas.org/downloads` is an Apache
directory listing of the official release archives and is the download location the project's own
documentation points to. Verified live on 2026-08-12: the listing carries 96 `.zip` files. Ten of
them are the numbered full IDL source archives — `spedas_1_00.zip`, `spedas_2_00.zip`,
`spedas_3_00.zip`, `spedas_3_1.zip`, `spedas_3_2.zip`, `spedas_4_0.zip`, `spedas_4_1.zip`,
`spedas_5_0.zip`, `spedas_6_0.zip`, `spedas_6_1.zip` — alongside the nightly source snapshot
`spdsw_latest.zip`, two historical source variants (`spedas_2_00_beta1.zip` dated 2016-05-31 and
`spedas_3_1_no.zip` dated 2018-10-29), the per-release platform bundles for users without an IDL
licence (`spedas_6_1_win64_85_109.zip`, `spedas_6_1_savefile_85.zip` and their equivalents back to
SPEDAS 1.0), and the two DLM installers `cdf_dlm.zip` and `geopack_dlm.zip`. The source-archive
family is the part that makes this URL the right Field 3 value. Carried over from the existing HSSI
record; no change.

**Rejected alternative: `https://github.com/spedas/bleeding_edge`.** This repository *is* in the
official `spedas` GitHub organization (org blog `www.spedas.org`), *is* IDL, and *is* actively
refreshed (last push 2026-08-10) — but its own `README.md` disqualifies it as the authoritative
source:

> "Github Mirror of IDL SPEDAS
>
> This repository contains a snapshot of the IDL SPEDAS 'bleeding edge' source code repository.
> It is periodically refreshed from the official repository, but we do not recommend installing it
> from here. Instead, go to one of the official download locations, to ensure that you're getting the
> latest official release, or the latest unofficial 'bleeding edge' snapshot"

The upstream repository it mirrors is a UC Berkeley SSL / UCLA Subversion server, and that server is
not publicly reachable. The evidence is the Subversion `$URL:` keyword expanded into the shipped
sources, of the form
`$URL: svn+ssh://thmsvn@ambrosia.ssl.berkeley.edu/repos/spdsoft/tags/spedas_6_1/... $`.
It is present in **2,845 of the archive's 5,882 `.pro` files (48%)**, and in 2,771 of the 5,610
outside `external/` (49%) — not in all of them, because whole bundled subtrees carry no SVN keywords
at all (`external/aacgm_v2/`: 0 of 7 `.pro` files; `external/astron/fits/`: 0 of 27) and even
first-party directories are mixed (`general/CDF/`: 19 of 31; `general/cotrans/`: 31 of 42). The
partial coverage does not weaken the conclusion: a keyword line naming that server appears in nearly
half the tree and in no other form, and no file names a public repository.

Neither the SPEDAS wiki `Main_Page` nor `Downloads_and_Installation` links to `bleeding_edge`; the only GitHub links on those pages are
`spedas/pyspedas` and `das-developers/das2dlm`.

Durable and useful context about the mirror even though it is not Field 3: its README states that
*"The IDL SPEDAS developers do monitor the Issues page for this repo"*, so it is the project's public
issue tracker.

Also rejected: `https://github.com/spedas/pyspedas` (separate software with its own HSSI record — the
Python implementation, not this one) and `https://github.com/das-developers/das2dlm` (one bundled
third-party component, `external/das2dlm/`, not this software).

### 4. Software Functionality (MANDATORY)

**Bounding rule for this field.** Each of the 56 values below is justified by at least one named
routine or directory in the 6.1 tree that exposes the capability to a user, and no single capability
is counted twice under one parent. Values are written `Parent: Child`; every child listed has its
parent listed, and every parent listed retains at least one child.

**Coordinate Transforms**
- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Ionospheric
- Coordinate Transforms: Planetary
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Heliospheric

**Data Processing and Analysis**
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: 3D Particle Distribution Processing
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Curlometer
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Linear Gradient Estimation
- Data Processing and Analysis: Packet Decommutation
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Wave Polarization Analysis
- Data Processing and Analysis: Wavelet Analysis

**Data Visualization**
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: 3D Graphics
- Data Visualization: Hodograms
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Movies
- Data Visualization: Orbit Plots
- Data Visualization: Spacecraft Formation Plots
- Data Visualization: Spectrogram

**Mission-related**
- Mission-related
- Mission-related: Analysis
- Mission-related: Calibration
- Mission-related: Distribution/Access
- Mission-related: Ingest
- Mission-related: Instrument Response
- Mission-related: Instrumentation
- Mission-related: Inventory
- Mission-related: Monitoring
- Mission-related: Operations
- Mission-related: Packet Decommutation
- Mission-related: Science Data Processing
- Mission-related: System Testing

**Models and Simulations**
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: Instrument Response
- Models and Simulations: Mission-Specific

**Evidence, value by value.**

*Coordinate Transforms.* `general/cotrans/cotrans.pro` documents its purpose as "geophysical
coordinate transformations" for GEI↔GSE, GSE↔GSM, GSM↔SM, GEI↔GEO, GEO↔MAG and GEI↔J2000, which is
**Magnetospheric**; `general/cotrans/special/fac/` (field-aligned) and
`general/cotrans/lmn_transform/gsm2lmn.pro` extend the same family. **Ionospheric** rests on
`general/cotrans/aacgm/` plus `external/aacgm_v2/` (AACGM-v2 with `igrf13coeffs.txt`) and the magnetic
local time converters `general/cotrans/sm2mlt.pro` and `tgsm2mlt.pro`. **Planetary** rests on
`general/cotrans/special/sse/sse_matrix_make.pro` and `sel_matrix_make.pro` (Selenocentric Solar
Ecliptic and Selenographic, i.e. lunar frames) and `general/misc/mso2lt.pro` (Mars Solar Orbital to
local time), with arbitrary IAU body frames reachable through SPICE. **Mission-Specific** rests on
`general/cotrans/spg2ssl.pro` (THEMIS spin-plane to spacecraft-solar-L-vector),
`projects/themis/spacecraft/fields/thm_efi_despin.pro`,
`projects/erg/satellite/erg/common/cotrans/erg_cotrans.pro` with `sga2sgi`/`sgi2dsi`/`dsi2j2000`, and
`general/spice/spice_vector_rotate.pro`, whose documented purpose is "Rotate a vector from one frame
to another frame" for any valid SPICE frame including spacecraft and instrument CK frames.
**Heliospheric** rests on `projects/SPP/COMMON/spice/spp_swp_spice.pro`, which computes and stores
spacecraft↔RTN quaternion rotations and their Euler angles (`SPP_QROT_SC2>RTN`,
`SPP_QROT_RTN>SC2_Euler_angles`), and on the same arbitrary-frame SPICE rotation machinery.

*Data Processing and Analysis.* **2D Slices**: `general/science/spd_slice2d/` and
`general/science/slice2d.pro`. **3D Particle Distribution Processing**:
`general/science/dist3d/dist3d__define.pro`, `general/science/spd_part_products/`,
`projects/themis/spacecraft/particles/thm_part_products/`, `projects/mms/particles/`.
**Calibration**: `projects/themis/spacecraft/fields/thm_cal_{fgm,efi,scm,fbk,fft,fit}.pro`,
`projects/themis/ground/thm_load_asi_cal.pro`, `general/missions/stereo/st_mag_cal.pro`,
`projects/mex/aspera/mex_asp_els_calib.pro`, `projects/SWFO/STIS/swfo_stis_cal_params.pro`.
**Curlometer**: `projects/mms/common/curlometer/mms_curl.pro` with
`projects/mms/examples/basic/mms_curlometer_crib.pro`. **Data Access and Retrieval**:
`general/spedas_tools/spd_download/spd_download.pro` ("Download one or more remote files and return
their local paths"), `general/misc/file_retrieve.pro`, `general/misc/file_http_copy.pro`, and several
hundred `*_load_*.pro` routines. **Data Reduction**: `general/tplot/auto_downsample.pro`,
`general/misc/reduce_timeres.pro`, `general/misc/time_average.pro`, `general/tools/tplot/avg_data.pro`,
`general/tplot/mplot_downsample_data.pro`. **Energy Spectra**: `general/science/spec3d.pro`,
`projects/themis/spacecraft/particles/thm_part_getspec.pro`, `general/science/wind/get_padspec.pro`.
**Field-line Tracing** (data-side): `external/IDL_GEOPACK/trace/{trace2iono,trace2equator,
ttrace2iono,ttrace2equator}.pro`, which trace tplot-variable positions to the ionosphere and the
equatorial plane. **File Format Conversion**: `general/CDF/tplot2cdf.pro` and `cdf2tplot.pro`,
`general/hdf/hdf2tplot.pro`, `general/netCDF/netcdf2tplot.pro`,
`general/hdf/hdf_to_cdfstruct.pro`, `projects/sosmag/sosmag_csv_to_tplot.pro`,
`projects/secs/eic_ascii2tplot.pro`. **Image Processing**:
`projects/themis/ground/thm_asi_create_mosaic.pro`, `thm_asi_merge_mosaic.pro`,
`thm_asi_recreate_mosaic.pro`, `thm_rego_create_mosaic.pro`,
`projects/themis/ground/asi_mosaic/thm_asi_imager_readfile.pro`, and the ERG OMTI chain
`projects/erg/ground/camera/{tabsint,tabsint_nobg,rm_star_absint,tasi2gmap,keogram_image}.pro`
(absolute-intensity calibration, star removal, geographic remapping, keograms), plus
`projects/emm/emm_emus_map_disk.pro`. **Linear Gradient Estimation**:
`projects/mms/common/curlometer/lingradest.pro` and `mms_lingradest.pro`.
**Packet Decommutation**: `projects/SWFO/STIS/swfo_ccsds_decom.pro`,
`swfo_stis_ccsds_header_decom.pro`, `ccsds_reader__define.pro`, `packet_reader__define.pro`,
`ptp_reader__define.pro`; `projects/swx/swx_ccsds_decom.pro`;
`projects/SPP/COMMON/spp_ccsds_pkt_handler.pro`, `spp_ptp_stream_read.pro`;
`projects/themis/spacecraft/fields/thm_fbk_decompress.pro`, `thm_fft_decompress.pro`;
`projects/themis/spacecraft/particles/thm_part_decomp16.pro`;
`projects/themis/spacecraft/particles/ESA/packet/`; and the C decommutation library
`projects/wind/3dp/wind_lib/` (`brst_dcm.c`, `p3d_dcm.c`, `pl_dcm.c`, `rates_dcm.c`, `sst_dcm.h`, …).
**Pitch Angle Distributions**: `general/science/pad.pro`, `padplot.pro`,
`projects/mms/fpi/mms_load_fpi_calc_pad.pro`, `general/science/wind/get_pad.pro`.
**Plasma Moments**: `general/science/{n_3d,v_3d,p_3d,t_3d,j_3d,je_3d,vth_3d}.pro`,
`projects/themis/spacecraft/particles/thm_cal_mom.pro`,
`general/missions/stereo/st_part_moments.pro`. **Spectrogram** (computation):
`general/misc/dpwrspc.pro`, `pwrspc.pro`, `tdpwrspc.pro`, `tpwrspc.pro`, and the multitaper package
`general/science/spd_mtm/`. **Time Series Analysis**: `general/misc/tsmooth_in_time.pro`,
`high_pass_filter.pro`, `thigh_pass_filter.pro`, `tdespike_ae.pro`, `simple_despike_1d.pro`,
`tinterpol.pro`, `ssl_correlate_tplot.pro`, `ssl_correlation_shift.pro`,
`general/tools/misc/spline_smooth.pro`,
`general/tools/tplot/deriv_data.pro`. **Wave Polarization Analysis**:
`general/science/wavpol/wavpol.pro` and `twavpol.pro` — "To perform polarisation analysis of three
orthogonal component time series data", returning degree of polarisation, wave normal angle,
ellipticity and helicity. **Wavelet Analysis**: `general/tools/tplot/wvlt/{wavelet,wavelet2,wav_data,
wavelet_data,wave_signif}.pro` with the GUI front ends `spedas_gui/utilities/spd_ui_wavelet.pro` and
`spedas_gui/panels/dproc/spd_ui_wavelet_options.pro`. **Analysis**: `general/science/
superpo_interpol.pro` and `superpo_histo.pro` compute the minimum, maximum and mean functions across
several time series at a specified resolution — the header gives "the calculation of AL (AU, AE)
indices" from an array of ground stations as its worked example — which is general scientific
analysis rather than any of the narrower techniques above. **Processing**: the tplot mini-language
calculator `general/mini/calc.pro`, which "takes a string as input and interprets the string as a
mini-language" able to manipulate tplot variables. These two are the broadest labels in this parent,
absorbing capability not captured by a more specific subcategory; each rests on its own routines
rather than sharing one citation.

*Data Visualization.* **Line Plots**: `general/tplot/tplot.pro`, `mplot.pro`, `pmplot.pro`,
`mplot_symlog.pro`. **Spectrogram** (display): `general/tplot/specplot.pro`,
`spedas_gui/display/spd_ui_make_spec.pro`. **2D Graphics**: `general/tplot/plotxyz.pro`,
`general/misc/plot_the_earth.pro`, `general/science/plot_map.pro`, the IUGONET
`overlay_map_*`/`plot_map_*` family, and `general/tplot/draw_color_scale.pro`. **2D Slices**:
`general/science/spd_slice2d/spd_slice2d_plot.pro`. **3D Graphics**: `spedas_gui/isee3d/`, the ISEE
3D / `stel3d` interactive three-dimensional distribution viewer (`isee_3d.pro`, `cube__define.pro`,
`polyhedron__define.pro`, `stel3d_widget_*`), plus `general/tplot/tplot3d.pro` and
`general/science/plot3d.pro`. **Hodograms**: `general/tplot/plotxy.pro` / `tplotxy`, whose documented
purpose is to take "an array of 3-d(Nx3) vectors or tplot variable and plots them using 2-d plots to
help visualize them", including projection of the data vectors "into a plane defined by the span of
the two custom vectors" — that is the hodogram construction, and it is the natural display for the minimum-variance frame produced by
`general/cotrans/special/minvar/minvar.pro` and `spedas_gui/panels/spd_ui_mva.pro`. Recorded with
the caveat that no routine in the tree is *named* "hodogram"; the capability is user-facing and
documented, but a reviewer who reads the subcategory more narrowly could reasonably strike it.
**Movies**: `general/spedas_tools/flipbookify/spd_flipbookify.pro` ("Turns the current tplot window
into a 'flipbook'"), `projects/maven/maven_orbit_tplot/maven_orbit_movie.pro`,
`projects/maven/sep/fov/mvn_sep_fov_movie.pro`, `projects/iugonet/plot/iug_movie_smart.pro`,
`projects/erg/ground/radar/superdarn/make_fanplot_pictures.pro`. **Orbit Plots**:
`projects/mms/mec/mms_orbit_plot.pro`, `projects/elfin/examples/elf_plot_orbits_crib.pro` and
`elf_plot_orbits_mercator_crib.pro`, `projects/maven/maven_orbit_tplot/maven_orbit_snap.pro`,
`projects/kaguya/general/kgy_orbit_snap.pro`, `general/spice/orrery.pro`.
**Spacecraft Formation Plots**: `projects/mms/mec/mms_mec_formation_plot.pro`,
`projects/mms/common/load_data/mms_load_tetrahedron_qf.pro`,
`projects/mms/examples/basic/mms_formation_crib.pro`. **Mission-Specific**:
`projects/goes/goes_overview_plot.pro`, `projects/goesr/goesr_overview_plot.pro`,
`projects/poes/poes_overview_plot.pro`, `projects/themis/ground/thm_gmag_stackplot.pro`,
`projects/maven/quicklook/mvn_spaceweather.pro`,
`projects/elfin/plots/epde_plot_wigrf_multispec_overviews.pro`,
`projects/secs/{eics,seca}_overlay_plots.pro`.

*Mission-related.* The distinguishing evidence is that SPEDAS is not only an analysis client but part
of at least one mission's ground system. **Operations**: `projects/mms/sdc/` implements the MMS
Scientist-in-the-Loop workflow end to end — `mms_sitl_login.pro`, `get_mms_sdc_connection.pro`,
`validate_mms_sitl_connection.pro`, `get_mms_{abs,gls,sitl}_selections.pro`, `get_mms_srois.pro`,
and crucially `submit_mms_sitl_selections.pro`, which writes burst selections *back* to the MMS
Science Data Center; the region-of-interest helper `projects/mms/sitl/bss/mms_get_roi.pro` sits in the
burst-segment-status subtree rather than in `sdc/`. **Analysis**: `projects/mms/sitl/eva/`, the Event
Visualization and Analysis SITL tool. **Inventory** rests on the MMS
burst-segment lifecycle catalogue and on nothing weaker. `get_mms_burst_segment_status.pro` queries
the SDC's `mms_burst_data_segment` dataset and returns one record per segment carrying
`dataSegmentId`, `fom`, `isPending`, `inPlayList`, `status`, `numEvalCycles`, `sourceId`,
`createTime`, `finishTime` and `discussion`; `mms_bss_list.pro`, `mms_bss_table.pro` and
`mms_bss_history.pro` then list, tabulate and account for those records by real lifecycle state —
`mms_bss_list`'s `/bad` path selects status `'trimmed subsumed deleted obsolete'` and its
`/overwritten` path selects `'DEMOTED DERELICT'`, while `mms_bss_history` sums segment sizes per
category against the onboard burst-buffer hard limit across the mission. A catalogue of mission data
products carrying states and transitions is what this label means. **The label holds only on that
basis, and the caveat belongs with it:** the file-side routines `get_mms_file_info.pro`,
`get_mms_file_names.pro` and `mms_files_in_interval.pro` do not support it and should not be cited
for it. The first two return file listings and sizes from the SDC `file_names`/`file_info` API, and
the third filters such a listing to a time range by parsing the timestamp out of each filename —
ordinary retrieval bookkeeping that any data client performs, already covered by `Data Processing and
Analysis: Data Access and Retrieval`. A later refresh that finds the burst-segment machinery gone
should drop `Inventory` rather than fall back on the file-listing routines. **Distribution/Access**:
`download_mms_files.pro`, `get_mms_science_file.pro`, `get_mms_ancillary_file.pro`,
`projects/emm/emm_file_retrieve.pro`, `projects/SWFO/STIS/swfo_file_retrieve.pro`.
**Science Data Processing**: `general/missions/rbsp/efw/l1_to_l2/`
(`rbsp_efw_make_l2.pro`, `rbsp_efw_make_l2_{esvy_despun,esvy_uvw,fbk,hsk,spec,spinfit,vsvy,
vsvy_hires}.pro`, `rbsp_efw_make_l3.pro`, with shipped CDF skeletons such as
`rbspa_efw-l2_spec_00000000_v01.cdf`), `general/missions/rbsp/efw/rbsp_phasef/file_production/`,
`projects/SWFO/STIS/swfo_stis_make_l0b.pro`, `projects/maven/l2gen/`,
`projects/maven/mvn_pf_make_cdf.pro`. **Ingest**: the telemetry stream/file readers
`projects/SPP/COMMON/{spp_ssr_file_read,spp_itf_stream_read,spp_ptp_stream_read,
spp_msg_stream_read}.pro` and `projects/SWFO/STIS/{swfo_ptp_file_read,swfo_gsemsg_lun_read,
swfo_ptp_lun_read}.pro`, which pull raw packets into the `apdat` data-product framework.
**Monitoring**: `projects/SWFO/STIS/swfo_init_realtime.pro`, `projects/swx/swx_init_realtime.pro`,
`projects/hermes/hermes_init_realtime.pro`, `general/misc/file_stuff/socket_reader__define.pro` and
`socket_recorder__define.pro`, `projects/SWFO/STIS/swfo_recorder.pro` and `swfo_ptp_recorder.pro`.
**Instrument Response**: `projects/SWFO/STIS/swfo_stis_inst_response.pro` plus
`_calval`, `_gpa`, `_peakeinc` and `_matmult_plot` variants;
`projects/themis/spacecraft/fields/thm_comp_{efi,eac,scm}_response.pro`;
`general/missions/rbsp/efw/rbsp_anti_aliasing_response.pro`. **Instrumentation**: the SWFO STIS
ground-support-equipment drivers `projects/SWFO/STIS/{gse_iongun_reader,gse_keithley,gse_keysight,
cmblk_keysight}__define.pro` and `swfo_stis_create_lut.pro`, `swfo_stis_adc_map.pro`. These read
bench hardware during pre-launch test and calibration rather than flight telemetry:
`gse_keithley__define.pro` describes itself as working "with the common block files to decommutate
data from Keysight power supplies", and subclasses `socket_reader` to parse a streaming ASCII line
into a current reading and two sense values. **Caveat on the basis:** this label rests on the
ground-support equipment of a single instrument subsystem. Every routine cited for it lives under
`projects/SWFO/STIS/`, and the only three `gse_*__define.pro` drivers in the tree are the SWFO STIS
ones named here. The entry is correct but narrow, and a refresh should re-examine it if that subtree
changes.
**Calibration**: the mission calibration pipelines already cited plus
`projects/SWFO/STIS/swfo_pulser_cal.pro` and
`projects/lomonosov/calibrate_lomo_engineering.pro`. **Packet Decommutation**: as above.
**System Testing**: the bundled unit-test framework `general/qa_tools/mgunit/`, the 52
`*_ut__define.pro` test objects in the tree (43 of them under `projects/`), `external/IDL_GEOPACK/geopack_validate.pro`,
`projects/themis/spacecraft/fields/thm_efi_sdt_test.pro`, and the cross-language harness
`general/spedas_tools/python_validation/spd_run_py_validation.pro`.

*Models and Simulations.* **Empirical**: `external/IDL_GEOPACK/` wraps N. A. Tsyganenko's external
magnetic field models with one directory each for `t89`, `t96`, `t01`, `t04s`, `ta15`, `ta16`, `ts07`,
plus `get_tsy_params.pro`, `calculate_lshell.pro`, `calc_pdyn.pro` and `tsy_valid_param.pro`;
`external/aacgm_v2/igrflib_v2.pro` with `igrf13coeffs.txt` implements IGRF-13; and
`general/misc/{neutral_sheet,mpause_2,mpause_t96,mpause_flag,bshock_2}.pro` with
`general/science/cal_bsn2.pro` and `general/science/get_bsn2.pro` implement neutral-sheet,
magnetopause and bow-shock boundary models. **Field-line Tracing**: the
GEOPACK `trace/` routines trace through that model field, which is model-side tracing as distinct
from the data-side entry under Data Processing and Analysis. **Instrument Response**: the SWFO STIS
response model, the THEMIS filter/ADC response models
(`bessel_filter_resp.pro`, `butterworth_filter_resp.pro`, `thm_adc_resp.pro`,
`thm_dfb_dig_filter_resp.pro`) and `projects/maven/sep/fov/`. **Mission-Specific**: the THEMIS spin
model `projects/themis/spin/`, whose `spinmodel_post_process.pro` constructs standard,
partially-corrected and fully-corrected eclipse spin-phase model objects for each probe and falls
back down that chain when the state CDFs lack the eclipse spin-model variables (with
`spinmodel_python_test.pro` exercising it), together with
`projects/themis/spacecraft/particles/thm_part_apply_eclipse.pro`, which applies the modelled eclipse
phase offset `eclipse_dphi` to 3D particle distribution structures. Two routines were considered for
this label and are deliberately not cited for it, because both merely load pre-computed output and
that is data access rather than modelling:
`projects/maven/maven_orbit_tplot/maven_orbit_predict.pro` selects one of six pre-generated SPICE
predict ephemeris kernels (`trj_orb_*.bsp`) and derives planning geometry from it, and
`general/missions/rbsp/efw/rbsp_load_emodel_cdf_file.pro` downloads and `cdf2tplot`s
`rbsp?_e_model_YYYY_MMDD_v01.cdf` files whose own header attributes them to a third party ("These CDF
files were created by Sheng Tian, 2020"). The label stands without them.

**Values considered and deliberately not recorded**, so a later refresh does not re-propose them:

- `Coordinate Transforms: Solar` — SPEDAS 6.1 has no solar-disk coordinate machinery. `Stonyhurst`,
  `helioprojective` and `heliographic` do not occur in any `.pro` file, and the three occurrences of
  `Carrington` are all non-transforms: a default solar rotation period in the Parker-spiral
  calculation of `general/spice/orrery.pro` ("Default = 25.38 days (i.e., Carrington)"), a
  `CARR_FILE` keyword in the retired `general/CDF/obsolete/loadallcdf.pro`, and a docstring in
  `projects/SPP/sweap/SPC/L3i/load/psp_load_swp.pro` noting that the PSP SPC L3i product *contains*
  "Carrington longitude/latitude data" — a quantity read out of a file, not one SPEDAS computes. The
  heliographic and heliocentric quantities it handles (`projects/SPP/fields/l1/l1_ephem/
  spp_fld_ephem_spp_{hg,hgi,hgmag,hgspec,hci,hee,heeq,hertn}_load_l1.pro`) are pre-computed ephemeris
  variables read out of PSP FIELDS L1 files, not transforms SPEDAS performs, and the frame rotations
  it does compute are heliospheric (RTN) rather than solar-surface.
- `Data Processing and Analysis: Data Assimilation` — no assimilation scheme, Kalman filter or
  observation-model blending in the tree.
- `Data Processing and Analysis: Magnetic Null Finding` — searched for "magnetic null", "null point"
  and "nulls" across all `.pro` files; the only hits are unrelated uses of the word "null" (IDL's
  `!null`, null pointers, null strings). SPEDAS ships the multi-spacecraft gradient tools
  (`lingradest`, `mms_curl`) that a null-finding method would build on, but not the method itself.
- `Data Processing and Analysis: ML/AI`, `Data Visualization: ML/AI`, `Mission-related: ML/AI`,
  `Models and Simulations: ML/AI` — no machine-learning code: searched for "neural network",
  "machine learning", "tensorflow", "random forest" and "deep learning" with no hits.
- `Data Visualization: Web-Based` — `spedas_gui/` is an IDL widget application, not a browser
  application. There is no HTML or JavaScript **application** front end, no embedded web server and
  no notebook-based visualization workflow. The tree does hold 16 `.html` files, but every one is
  static documentation — `help.html`, `help_list.html` and `3dp_ref_man.html` duplicated across
  `general/{key_param,misc,science,tplot}/` and `projects/wind/3dp/idl/`, plus
  `general/science/spd_mtm/spd_mtm_v1_help.html`. There are no `.js` files at all, and the sole
  `.ipynb` (`general/misc/system/CSV_Color_Tables/make_csv/colormap_export.ipynb`) is an unrelated
  colormap-CSV build helper rather than a visualization workflow.
- `Mission-related: Archive`, `Infrastructure as Code`, `Orchestration`,
  `Observatory/Instrument Models` — SPEDAS reads from mission archives but does not implement one;
  there are no infrastructure or workflow-orchestration definitions; and the observatory/instrument
  modelling it does do is instrument-response modelling, already recorded under
  `Mission-related: Instrument Response` and `Models and Simulations: Instrument Response`.
- `Mission-related: Processing` — the only mission ground-system processing in the tree is the
  production of science data products at defined levels: `general/missions/rbsp/efw/l1_to_l2/` and
  `general/missions/rbsp/efw/rbsp_phasef/file_production/`,
  `projects/SWFO/STIS/swfo_stis_make_l0b.pro`, `projects/maven/l2gen/` and
  `projects/maven/mvn_pf_make_cdf.pro`. Those are precisely the routines that justify
  `Mission-related: Science Data Processing`, which is the more specific and therefore the correct
  label; no mission-related processing capability distinct from science-data-level production exists
  in the tree. Recording the generic `Processing` label alongside the specific one would count one
  capability twice under a single parent, so only `Science Data Processing` is recorded. Note that
  `Data Processing and Analysis: Processing` is a **different** value with its own independent basis
  — the tplot mini-language calculator `general/mini/calc.pro` — and is correctly recorded.
- `Models and Simulations: MHD`, `First Principles`, `Physics-Based`, `Data Guided`, `Forecasting`,
  `Forward-Fitting`, `Theory`, `Observatory/Instrument Models` — SPEDAS offers no simulation solver as
  a capability of the software. `projects/maven/maven_orbit_tplot/mhd_orbit.pro` and
  `hybrid_orbit.pro` are named for the simulations whose output they *overlay*: the entire content of
  `mhd_orbit.pro`'s header `PURPOSE:` field is the single word "Plots", and the routine draws
  longitude/latitude tracks on a MAG-MOLA Mars map. The Tsyganenko and IGRF models are
  empirical/semi-empirical field representations, fully covered by `Empirical`; adding
  `Physics-Based` alongside would double-count the same routines.

  The closest near-miss is `projects/maven/models/sep_elec/`, and it is recorded here so a later
  refresh neither rediscovers it as new evidence nor re-litigates it. `mvn_sep_elec_peri_model.pro` is
  a MAVEN SEP electron backtracer: it loads a pre-computed MHD/crustal magnetic-field dataset through
  `mvn_sep_elec_peri_mhd.pro`, forms the residual between the measured 1-second field and that dataset
  (`magres = magit - mvn_sep_elec_peri_bcrust(...)`), then integrates relativistic electron
  trajectories through the combination with `mvn_sep_elec_traj_solver.pro` while accumulating CO2
  optical depth along each path. In spirit that is data-guided physics, and `mvn_sep_elec_traj_solver`
  is a genuine analytic gyro-motion integrator — so this exclusion deliberately does **not** rest on a
  claim that the tree contains no integrator anywhere, which would be false. It rests on the subtree
  not being a capability the software offers to anyone. Every entry point restores its field dataset
  from one researcher's personal home directory: `/home/rahmati/Desktop/crustalb/` is hard-coded in
  `mvn_sep_elec_peri_mhd.pro`, `mvn_sep_elec_peri_model.pro`, `mvn_sep_elec_peri_stats.pro`,
  `mvn_sep_elec_load_bcrust.pro` and `mvn_sep_elec_rotate_bcrust.pro`, so the code cannot run for any
  other user. `mvn_sep_elec_peri_model` ends in a bare `stop`, an interactive debugging halt. Nothing
  outside that one directory calls into it — the sole apparent outside hit,
  `projects/maven/sep/mvn_sep_pad.pro`, is a coincidental substring match on `sep_electron_*` tplot
  variable names, not a call. There is no crib, no `*_ut__define.pro` test object and no documentation
  for it anywhere in the tree. It is a personal research leftover that shipped in the release archive,
  not a modelling capability of SPEDAS, so the three labels stay excluded.
- `Servers and Environments` and `Servers and Environments: Distribution/Access` — **not recorded,
  correcting a previously stored value that was wrong.**
  `Servers and Environments: Distribution/Access` was stored in this software's HSSI record and it
  does not describe SPEDAS. The category covers server implementations and data-serving endpoints;
  SPEDAS provides neither. The routines that had been read as supporting it are purely
  consumption-side, and reading them settles the question rather than leaving it to judgement.
  `general/spedas_tools/spd_download/spd_download.pro` states its purpose as "Download one or more
  remote files and return their local paths", and its body does exactly that and only that: for each
  URL matching `^(http|ftp)s?://` it calls `spd_download_file`, otherwise it treats the reference as a
  local resource and calls `spd_copy_file`, then returns the list of local paths.
  `spd_get_proxy.pro` reads the `http_proxy` environment variable and appends
  `proxy_hostname`/`proxy_port`/`proxy_username`/`proxy_password` to a structure "for use with
  idlneturl" — that configures SPEDAS's own *outbound* requests, not any inbound service. The
  `*_read_config.pro` / `*_write_config.pro` / `*_config_filedir.pro` machinery cited alongside them
  (present in 16 of the 37 top-level `projects/` subtrees, with equivalents under `general/`) points
  SPEDAS *at* local or mirrored data stores, which is consumption-side for the same reason. Nothing in
  the tree serves or distributes data to a consumer: IDL's `socket` procedure is client-only, all 13
  of its call sites in the tree pass a remote host, a port and a `connect_timeout` (for example
  `general/misc/file_http_copy.pro`, `general/tools/misc/recorder.pro`,
  `projects/SWFO/STIS/swfo_ptp_recorder.pro`), and `socket_reader__define.pro` documents itself as a
  tool that "opens a socket and reads streaming data from a server (host)". The capability SPEDAS
  actually has — fetching data over the network and making mission files available locally — is
  already recorded twice, under `Data Processing and Analysis: Data Access and Retrieval` and
  `Mission-related: Distribution/Access`.

  The parent `Servers and Environments` was never stored, so the child sat in the record without it.
  That orphan is resolvable two ways and removing the child is the correct one: supplying the parent
  would assert something strictly stronger than the unsupported child alone — that SPEDAS provides
  server or environment infrastructure as a top-level capability — and the tree supports neither
  claim. A future agent that notices the missing parent should therefore not repair the schema by
  adding it.
- `Servers and Environments: Data servers processing and handling` — no server implementation. There
  is no listening socket anywhere in the tree; `socket_reader__define.pro` and
  `swfo_init_realtime.pro` are *clients* that connect out to a telemetry stream.
- `Servers and Environments: High Performance Computing` — no MPI, OpenMP or job-scheduler code
  (searched for `mpi_`/`openmp`; the single hit, `projects/maven/mvn_orb_ql/mvn_orbql_symcat.pro`, is
  an unrelated substring match in a symbol catalogue).
- `Servers and Environments: Software or Environment Container` — no Dockerfile, Singularity
  definition or container recipe in the tree.

### 5. Related Region (MANDATORY)

- Earth Magnetosphere
- Earth Inner Magnetosphere
- Earth Outer Magnetosphere
- Earth Magnetotail
- Earth Magnetosheath
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Thermosphere
- Earth Atmosphere
- Earth Lower and Middle Atmosphere
- Solar Wind
- Interplanetary Space
- Solar Environment
- Planetary Magnetospheres
- Mars Magnetosphere
- Saturn Magnetosphere
- Jupiter Magnetosphere

`Earth Magnetosphere`, `Interplanetary Space`, `Planetary Magnetospheres` and `Solar Environment`
carry over from the existing HSSI record; the rest are additions. The addition rationale is to record
the more specific regions the vocabulary offers alongside the broad ones the submitter chose, rather
than in place of them.

- **Earth Inner Magnetosphere** — the Van Allen Probes tree `general/missions/rbsp/{ect,efw,emfisis,
  rbspice}/`, the ELFIN tree `projects/elfin/`, `external/IDL_GEOPACK/calculate_lshell.pro`, and
  `projects/mica/mica_load_induction.pro`.
- **Earth Outer Magnetosphere** — the magnetopause models `general/misc/mpause_2.pro`,
  `mpause_t96.pro`, `mpause_flag.pro`, and the dayside THEMIS/MMS/Cluster instrument suites.
- **Earth Magnetotail** — `general/misc/neutral_sheet.pro` (magnetotail neutral-sheet models),
  `projects/geotail/`, `projects/cluster/`, and THEMIS/ARTEMIS tail science support.
- **Earth Magnetosheath** — the bow-shock model and shock-normal tools `general/misc/bshock_2.pro`,
  `general/science/cal_bsn2.pro` and `get_bsn2.pro`, with the MMS and Cluster suites.
- **Earth Auroral Subregion** — the all-sky imager chains `projects/themis/ground/thm_load_asi.pro`,
  `thm_load_ask.pro`, `thm_asi_create_mosaic.pro`, `thm_load_rego.pro` (Red-line Emission Geospace
  Observatory), `projects/erg/ground/camera/erg_load_camera_omti_asi.pro`,
  `projects/iugonet/load/iug_load_asi_nipr.pro`, plus `thm_make_ae.pro`/`thm_load_pseudoae.pro`.
- **Earth Ionosphere** — AACGM/MLT conversion, ionospheric field-line footpoints
  (`external/IDL_GEOPACK/trace/trace2iono.pro`), the Spherical Elementary Current Systems plug-in
  `projects/secs/` (equivalent ionospheric currents), ICON IVM and FUV
  (`projects/icon/load/icon_load_data.pro`), SuperDARN
  (`projects/erg/ground/radar/superdarn/erg_load_sdfit.pro`),
  `projects/iugonet/load/iug_load_ionosonde_rish.pro`, `iug_load_gps_atec.pro` and
  `iug_load_eiscat.pro`.
- **Earth Thermosphere** — ICON MIGHTI, whose thermospheric wind and temperature products
  `icon_load_data.pro` loads for both MIGHTI-A and MIGHTI-B
  (`projects/icon/examples/icon_crib_mighti.pro`).
- **Earth Atmosphere** — the BARREL balloon X-ray payloads `projects/barrel/barrel_load_{fspc,mspc,
  sspc,rcnt}.pro` measure bremsstrahlung produced by electrons precipitating into the atmosphere; the
  POES loader `projects/poes/poes_load_data.pro` provides `ted_ele_eflux_atmo`,
  `ted_pro_eflux_atmo` and `ted_total_eflux_atmo`, explicitly "atmospheric integral energy flux …
  at 120 km".
- **Earth Lower and Middle Atmosphere** — the IUGONET radar and weather-station set
  `projects/iugonet/load/iug_load_ear_trop_{nc,txt}.pro` (Equatorial Atmosphere Radar troposphere
  modes), `iug_load_blr_rish.pro` (boundary-layer radar), `iug_load_ltr_rish.pro` (lower-troposphere
  radar), `iug_load_meteor_*_nc.pro` (mesospheric meteor radars),
  `iug_load_aws_{id,ktb,rish,sgk}.pro` (automatic weather stations),
  `iug_load_gps_{champ,cosmic}_fsi_nc.pro` (GPS radio-occultation profiles).
- **Solar Wind** — the upstream monitors: ACE (`general/key_param/load_ace_{mag,swepam,epam,sis,cris,
  uleis,sepica}.pro`), Wind (`general/key_param/load_wi_{mfi,swe,3dp,wav,epa}.pro`,
  `projects/wind/3dp/`), DSCOVR (`projects/dscovr/load/dsc_load_{fc,mag}.pro`), OMNI
  (`projects/omni/omni_load_data.pro`), PSP SWEAP, and
  `external/IDL_GEOPACK/calc_pdyn.pro` (solar-wind dynamic pressure).
- **Mars Magnetosphere** — MAVEN (`projects/maven/`, ten instrument subtrees), Mars Express
  (`projects/mex/aspera/`), Emirates Mars Mission (`projects/emm/`).
- **Saturn Magnetosphere** — `projects/cassini/das2dlm_load_cassini_mag_*.pro` and
  `das2dlm_load_cassini_rpws_*.pro`, which are ordinary loaders rather than example cribs.
- **Jupiter Magnetosphere** — `projects/juno/juno_load_data.pro` with `das2tplot.pro` and
  `das_xml_parser__define.pro`, which query a das2 server for Juno datasets.

**Regions considered and not recorded:** `Corona`, `Chromosphere`, `Photosphere` and
`Solar Interior` — SPEDAS 6.1 does none of the solar remote sensing those regions imply. It has no
solar image analysis, no coronal modelling, no magnetogram handling, and does not support STEREO
SECCHI or SOHO's imagers. GOES XRS support (`projects/goesr/goesr_load_data.pro` datatype `'xrs'`)
is a full-disk soft X-ray *irradiance* time series, which `Solar Environment` already covers.
`Heliosheath` — no Voyager, IBEX or outer-heliosphere support. `Uranus Magnetosphere` and
`Neptune Magnetosphere` — no support of any kind. `Earth Magnetosphere` is retained alongside its
four sub-regions rather than being replaced, because SPEDAS's magnetospheric coverage is general
rather than confined to those four.

### 6. Authors (MANDATORY)

Twelve authors, matching the author list the project itself publishes. The authoritative source is
the 6.1 Zenodo deposit's `creators` array (`https://zenodo.org/api/records/15023025`), which the
SPEDAS wiki reproduces — same twelve names, same order — as the recommended citation:
*"Angelopoulos, V., Lewis, J.,
McTiernan, J., Grimes, E., Russell, C., Drozdov, A., Cruce, P., Hatzigeorgiu, N., Wu, J., Larson, D.,
McFadden, J., & Flores, A. (2024). SPEDAS (Space Physics Environment Data Analysis System) (6.1).
Zenodo."* The twelve already stored in HSSI are exactly this set, so this is a union with no
additions and no removals.

| Given name | Family name | ORCID | Affiliation(s) (ROR) |
|---|---|---|---|
| Vassilis | Angelopoulos | https://orcid.org/0000-0001-7024-1561 | University of California, Los Angeles (https://ror.org/046rm7j60) |
| Patrick | Cruce | *none* | University of California, Los Angeles (https://ror.org/046rm7j60) |
| Alexander | Drozdov | https://orcid.org/0000-0002-5334-2026 | University of California, Los Angeles (https://ror.org/046rm7j60) |
| Aaron | Flores | *none* | *none* |
| Eric | Grimes | https://orcid.org/0000-0001-5756-8789 | Adnet Systems (United States) (https://ror.org/05we1n045) |
| Nick | Hatzigeorgiu | *none* | Space Sciences Laboratory, University of California, Berkeley (https://ror.org/048400679); University of California, Berkeley (https://ror.org/01an7q238) |
| Davin | Larson | https://orcid.org/0000-0001-5030-6030 | Space Sciences Laboratory, University of California, Berkeley (https://ror.org/048400679); University of California, Berkeley (https://ror.org/01an7q238) |
| Jim | Lewis | https://orcid.org/0009-0005-4191-5906 | Space Sciences Laboratory, University of California, Berkeley (https://ror.org/048400679); University of California, Berkeley (https://ror.org/01an7q238) |
| James | McFadden | *none* | Space Sciences Laboratory, University of California, Berkeley (https://ror.org/048400679); University of California, Berkeley (https://ror.org/01an7q238) |
| James | McTiernan | https://orcid.org/0000-0002-3038-176X | Space Sciences Laboratory, University of California, Berkeley (https://ror.org/048400679); University of California, Berkeley (https://ror.org/01an7q238) |
| Cindy | Russell | *none* | University of California, Los Angeles (https://ror.org/046rm7j60) |
| Jiashu | Wu | *none* | University of California, Los Angeles (https://ror.org/046rm7j60) |

**Patrick Cruce's affiliation comes from the reference publication, not from the deposit.** HSSI
stored him with no affiliation, faithfully reflecting Zenodo, where his `affiliation` field is
`null`. The reference publication supplies it: the Europe PMC full record for
`10.1007/s11214-018-0576-4` (PMC6380193) gives Cruce P as
*"Department of Earth, Planetary and Space Sciences, and Institute of Geophysics and Planetary
Physics, University of California, Los Angeles, USA"*. Recording `University of California, Los
Angeles` (ROR `https://ror.org/046rm7j60`) rather than the department, because that ROR is the
institutional level already used for Angelopoulos, Drozdov, Russell and Wu, avoiding a separate
department-level near-duplicate.

**Aaron Flores's affiliation remains empty, deliberately.** Zenodo gives `null`; he is not an author
of the 2019 reference publication, so Europe PMC cannot supply it; and no other primary source names
his institution. An inference from his co-authors would be a guess.

**No ORCIDs can be added for the six authors who lack them.** Searched the ORCID public API for each:
"Patrick Cruce" returns no record at all (eight `Cruce` records, none with the given name Patrick);
"Hatzigeorgiu" returns zero records; "James McFadden" returns two, one at an orthopaedic institute
and one with no institution listed, neither confirmable as the UC Berkeley space physicist; "Jiashu
Wu" returns five, none at UCLA; "Cindy Russell" returns one with a garbled name and no institution.
Assigning any of these would be a guess. This is a negative result, not an unfinished search — a
later refresh should not repeat it unless the authors register ORCIDs.

**Eric Grimes's earlier UCLA affiliation was considered and not added.** The 2019 reference
publication places him at UCLA, but the 2024 Zenodo deposit — the authoritative source for this
release's authorship — places him at Adnet Systems, and HSSI stores Adnet. Adding UCLA would record a
superseded affiliation as current.

**Reference-publication co-authors are correctly *not* authors here.** The 2019 SSR paper has 102
authors in Crossref's record, including several SPEDAS contributors (D. A. King, D. A. Roberts, J. B.
Faden, M. Galloy and others). Field 6 records the software's authors, and the project's own release
citation names the twelve above. The paper's wider author list belongs to Field 14.

### 7. Software Name (MANDATORY)
`SPEDAS (Space Physics Environment Data Analysis System)`

Carried over from the existing HSSI record unchanged. It matches the Zenodo deposit's `title` exactly
and the form the project uses in its own citation. Considered and rejected: the bare acronym
`SPEDAS`, and the wiki's occasional expansion "Space Physics Environment Data Analysis **Software**"
(`Main_Page`: "the Space Physics Environment Data Analysis Software (SPEDAS) framework"). The stored
name is the deposit's own title and the submitter's deliberate wording; a stylistic preference is not
grounds to change it.

### 8. Description (MANDATORY)
`SPEDAS (the Space Physics Environment Data Analysis System) is a set of tools, implemented in the IDL programming language, to locate, download, analyze, and visualize space-based and ground-based data sets of interest to heliophysics researchers.`

Carried over from the existing HSSI record unchanged. It is accurate against the 6.1 tree — locating
and downloading (`spd_download`, hundreds of `*_load_*`), analysing (`general/science/`,
`general/tools/`) and visualising (`general/tplot/`, `spedas_gui/`) both space-based (`projects/`) and
ground-based (`projects/themis/ground/`, `projects/iugonet/`, `projects/secs/`, `projects/bas/`,
`general/missions/kyoto/`) data — and it correctly identifies IDL, which is the distinction between
this record and the PySPEDAS record. The wording is the submitter's and is retained deliberately.

### 9. Concise Description (OPTIONAL)
`SPEDAS (the Space Physics Environment Data Analysis System) is a set of IDL tools for working with heliophysics-related data sets.`

Carried over from the existing HSSI record unchanged, for the same reasons as Field 8.

### 10. Publication Date (RECOMMENDED)
`2014-08-27`

Carried over from the existing HSSI record and confirmed correct. This is the software's first
release, corroborated twice: the earliest version DOI in the Zenodo concept,
`10.5281/zenodo.14919976` (version 1.0), carries `Issued` `2014-08-27`; and the downloads page's
`spedas_1_00.zip` is dated 2014-08-27. No change.

Note the distinction from Field 12: Field 10 is the first publication of the software, Field 12's
release date is the current version's. They are correctly different dates.

### 11. Publisher (RECOMMENDED)
`Zenodo` — identifier `https://zenodo.org`

Carried over from the existing HSSI record. Zenodo is the publisher of record for the DOI in Field 2,
and DataCite reports `publisher: Zenodo` for both the concept DOI and the 6.1 version DOI. Considered
and rejected: the University of California, Berkeley Space Sciences Laboratory and UCLA IGPP, which
host and develop the software but are not the publisher of the cited deposit.

### 12. Version (RECOMMENDED)

- **Version number:** `6.1`
- **Version release date:** `2024-06-12` — **corrects the stored `2025-03-14`**
- **Version PID:** `https://doi.org/10.5281/zenodo.15023025`
- **Version description:** same text as Field 8

**6.1 is the current stable release; the version number does not change.** Four independent
confirmations: `spedas_6_1/spedas_version.txt` contains exactly two lines, `6.1` and `May 2024`; the
wiki `Downloads_and_Installation` heads its page "*New* SPEDAS 6.1 released (May 2024)" and states
"The QA process for SPEDAS 6.1 has now been completed, and this version of the software is now
released for general use for users who have paid for IDL licenses"; the downloads directory's newest
numbered full-source archive is `spedas_6_1.zip` with no 6.2 or later present; and the newest version
DOI under the concept `10.5281/zenodo.14919975` is `10.5281/zenodo.15023025`, version `6.1`.

**The stored release date `2025-03-14` was wrong; the release date is `2024-06-12`.** `2025-03-14` is
the date the *Zenodo record was created* during the project's 2025 retro-deposit of its release
history, not a release date: `https://zenodo.org/api/records/15023025` reports `created:
2025-03-14T05:57:49` while the same record's `publication_date` is `2024-06-12`. It reached HSSI as a
DOI-autofill artifact. `2024-06-12` is the only day-precision authoritative date available and it is
corroborated twice independently — the archive's HTTP `Last-Modified` is `Wed, 12 Jun 2024 20:24:30
GMT`, and DataCite reports `{'date': '2024-06-12', 'dateType': 'Issued'}` for the 6.1 DOI.

**Residual discrepancy, recorded honestly.** The package's own `spedas_version.txt` stamps the release
"May 2024" (month precision only) and the wiki announces it as May 2024, while the published archive
and the DOI both date to 2024-06-12 — presumably the gap between completing QA and publishing the
archive. No May day-of-month is available from any source, so inventing one would be fabrication;
`2024-06-12` is used because it is the only day-precision date that any authoritative source states.

**Rejected alternative: the nightly build `spdsw_latest.zip`.** It is newer (2026-08-11, ~86 MB) and
is served from the same downloads directory, but the wiki explicitly disqualifies it as a release:
"you can download the nightly build instead of the SPEDAS 6.1 release. This is built every day and it
contains the most recent source code, but it is **untested** and you may encounter bugs and unresolved
problems." Treating it as the version would misrepresent an untested snapshot as a stable release.

**Caveat about a stale upstream page.** The wiki `Main_Page` still contains the sentence "The most
current version, SPEDAS 6.0, was released in December 2023," which contradicts the same page's own
Downloads section ("New! SPEDAS 6.1 released (May 2024)") and the `Downloads_and_Installation` page.
The main-page sentence is stale prose that the maintainers did not update; it is not evidence that 6.0
is current. A later refresh reading only `Main_Page` could be misled by it.

**Presentation artifact, not a value.** The catalogue displays this version as
`"SPEDAS (Space Physics Environment Data Analysis System) - 6.1"` by prefixing the software name.
The canonical version number remains the bare string `6.1`.

### 13. Programming Language (RECOMMENDED)

- IDL
- C

`IDL` carries over from the existing HSSI record; `C` is an addition. 5,882 of the 6,996 files in the
tree are `.pro` IDL sources, so IDL is unambiguous. `C` is warranted by
`projects/wind/3dp/wind_lib/`, a 75-`.c`/69-`.h` telemetry-decommutation library
(`3dpfile.c`, `brst_dcm.c`, `p3d_dcm.c`, `pl_dcm.c`, `rates_dcm.c`, `sst_steps.c`, `sst3dmap.c`,
`map_22d.c`, `scan_index.c`, `cdf_time.c`, …) that is compiled and shipped as
`projects/wind/3dp/idl/wind3dp_lib_{linux_x86_64,linux_x86,darwin_x86_64,darwin_i386,darwin_ppc,
sunos_sparc}.so` and invoked from IDL through `call_external`, for example
`num = call_external(wind_lib,'ospc_to_idl')` in `projects/wind/3dp/idl/get_ospc.pro` and
`call_external(wind_lib,'get_pmom_data')` in `get_pmom.pro`.

Considered and not recorded: the 13 `.sh` and 3 `.csh` shell scripts (SPEDAS/THEMIS environment setup
such as `projects/themis/setup_themis_bash`) — shell is not a value in the HSSI vocabulary, and these
are installation helpers rather than part of the software's implementation. `Python` is **not**
recorded: the tree contains no `.py` files. The Python that appears in
`general/spedas_tools/python_validation/` is inline script text passed to an external interpreter for
cross-validation against PySPEDAS, which is an interoperability relationship (Field 30), not a second
implementation language.

### 14. Reference Publication (RECOMMENDED)
`https://doi.org/10.1007/s11214-018-0576-4`

Carried over from the existing HSSI record and confirmed correct. Angelopoulos, V. et al., "The Space
Physics Environment Data Analysis System (SPEDAS)", *Space Science Reviews* 215(1), published
2019-01-22 (Crossref). Two independent confirmations that this is *the* paper for the software:
DataCite records `IsDescribedBy 10.1007/s11214-018-0576-4` on both the concept and the 6.1 version
DOI; and the SPEDAS wiki's "Citing SPEDAS" section names only this paper. No change.

### 15. License (RECOMMENDED)
`MIT License`

The HSSI record previously carried no license value; `MIT License` is the vocabulary's exact row name
for the licence the archive declares.

Primary evidence is the archive's own `LICENSE.txt`, which opens: "Unless otherwise indicated, the
following MIT license terms apply to the SPEDAS source code: MIT License / Copyright (c) 1990-2022 UC
Regents, unless otherwise indicated". DataCite corroborates with SPDX `rightsIdentifier: mit`,
`rights: MIT License`, `rightsUri: https://opensource.org/licenses/MIT`; the Zenodo record reports
`license: {'id': 'mit-license'}`.

**Durable licensing nuance a prospective user needs.** That same `LICENSE.txt` carves out four
bundled third-party components under other terms:

| `LICENSE.txt` names | Terms | Present in the 6.1 tree? |
|---|---|---|
| `external/das2pro/` | MIT (Copyright 2019 David Pisa, Larry Granroth) | **No such path exists.** The das2 component in 6.1 is `external/das2dlm/`; `das2pro` appears nowhere in the archive except in `LICENSE.txt` itself. |
| `external/aacgm_v2/astaog.pro` | GPL v2 or later (Kile B. Baker, National Science Foundation) | **Not under that filename.** The file is `external/aacgm_v2/astalg.pro` ("Author: R.J.Barnes (Based on C routines by Kile Baker)"), and the same notice is repeated verbatim in `external/aacgm_v2/LICENSE-AstAlg.txt` beside it, so `astaog` is a typo for `astalg`. |
| `projects/mms/sdc/test_tools/mgunit.sav` | BSD-type licence (Michael Galloy) | Yes. |
| `external/spdfcdas/` and `external/spdfssc/` | NASA Open Source Agreement 1.3 | Yes, both. |

The record's single `MIT License` value describes the SPEDAS code itself, which is the correct reading
of the field, but a redistributor must honour those carve-outs — and must resolve the two stale paths
by content rather than by name. The two mismatches are recorded because a redistributor auditing the
licence file by path will otherwise conclude the carve-outs do not apply.

**Second durable limitation, unrelated to the licence but decisive for a prospective user.** SPEDAS
runs on IDL, a commercial product. Full command-line use requires a paid IDL licence. The wiki
`Downloads_and_Installation` states the alternatives for users without one: "you can either use the
self-contained executables we provide, or you can separately install the IDL Virtual Machine (VM) and
use the save file we provide". So the GUI is usable without an IDL licence, but the source
distribution recorded in Field 3 is not.

Considered and rejected: `Other` (the licence is a standard, named one) and `Restricted` (the SPEDAS
code is not restricted; only the IDL runtime is commercial, which is a dependency property, not this
software's licence).

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

68 keywords. Canonical terms are lowercase; the catalogue presents the same terms in Title Case, so
they are listed here in canonical form.

Zenodo-derived terms (56): `aacgm`, `ace`, `akebono`, `arase`, `artemis`, `aurora`, `barrel`,
`cdaweb`, `cdf`, `cluster`, `coordinates`, `das2`, `data access`, `dscovr`, `elfin`, `equator s`,
`erg`, `fast`, `fields`, `geomagnetic`, `geotail`, `gmag`, `goes`, `ground magnetometer`, `gui`,
`hapi`, `heliophysics`, `heliosphere`, `icon`, `image`, `iugonet`, `kompsat`, `kyoto dst`,
`line plots`, `magnetic field modeling`, `magnetosphere`, `maven`, `mica`, `mms`, `moments`,
`parker solar probe`, `particles`, `plasma`, `plotting`, `poes`, `polar`, `psp`, `rbsp`,
`solar orbiter`, `solar wind`, `solo`, `space weather`, `spectrogram plots`, `themis`,
`van allen probes`, `wind`.

Additional evidence-based terms (12): `idl`, `stereo`, `superdarn`, `omni`, `spice`, `tsyganenko`, `geopack`,
`radiation belts`, `wavelet analysis`, `pitch angle distributions`, `ephemeris`, `netcdf`.

The stored 56 are the Zenodo deposit's own keyword list, transferred by DOI autofill; comparing
normalized (lowercased) forms, the two sets agree except that Zenodo has `equator-s` where HSSI
stored `equator s`. Keywords are HSSI's only open vocabulary, so "correcting" the hyphen would create
a second keyword row for the same concept rather than fixing one; the stored form is left alone and
the difference recorded here so it is not mistaken for a missing keyword.

Each of the 12 additional terms fills a real gap: `idl` is the single most distinguishing term for
this record versus the PySPEDAS record and was absent; `stereo` names a supported mission
(`general/missions/stereo/`) absent from the Zenodo-derived list; `superdarn`
(`projects/erg/ground/radar/superdarn/`), `omni` (`projects/omni/`), `spice`
(`general/spice/`, `external/IDL_ICY/`), `tsyganenko` and `geopack` (`external/IDL_GEOPACK/`),
`wavelet analysis` (`general/tools/tplot/wvlt/`), `pitch angle distributions`
(`general/science/pad.pro`), `ephemeris` (the `*_load_state`/`*_load_or` family), `netcdf`
(`general/netCDF/`, `projects/SWFO/STIS/swfo_ncdf_create.pro`) and `radiation belts` (the RBSP, ELFIN
and BARREL trees) each name a capability or supported dataset with dedicated code.

Considered and not added: an all-sky-imager keyword. The vocabulary carries three near-duplicate rows
(`All-sky imager`, `all-sky-camera`, `all-sky-imager`) and nothing in the sources selects among them,
so any pick would be arbitrary; `aurora` and `image` are already stored. Also not added: `IDL SPEDAS`
— a row that exists but is self-referential for this record.

Note on a stored keyword that the code does not support: `image` came from Zenodo's `IMAGE`, which
appears to name the IMAGE mission, but the 6.1 tree contains no IMAGE loader (see Field 32). It is
retained because keywords are the right home for a project-asserted association that the controlled
instrument/observatory vocabulary must not receive without code evidence.

### 17. Data Sources (OPTIONAL)

- CDAWeb
- das2
- FTP/FTPS Directories
- GFZ
- HAPI
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- SSCWeb
- TAP
- WDC

Nine values carry over from the existing HSSI record; `GFZ` and `WDC` are additions.

- **WDC** — `general/missions/kyoto/kyoto_load_dst.pro` and `kyoto_load_ae.pro` set
  `remote_data_dir='https://wdc.kugi.kyoto-u.ac.jp/'`, the Kyoto World Data Center for Geomagnetism,
  and print its data-use acknowledgement; `projects/iugonet/load/iug_load_gmag_wdc*.pro` read the WDC
  formats documented at `wdc.kugi.kyoto-u.ac.jp/mdplt/format/wdcformat.html`.
- **GFZ** — `general/missions/noaa/noaa_load_kp.pro` has a `/gfz` keyword that sets
  `kp_mirror = 'ftp://ftp.gfz-potsdam.de/'` with `remote_kp_dir = 'pub/home/obs/kp-ap/wdc/yearly/'`,
  and automatically switches to it: "Endtime is on or after 2018. Data will be loaded from
  ftp.gfz-potsdam.de". `projects/elfin/load_data/elf_load_kp.pro` documents the same GFZ Kp source.

**`TAP` is a retained stored value, and the Cluster Science Archive loader is what justifies it.**
ESA's Cluster Science Archive is reached through its TAP (Table Access Protocol) service layer:
`projects/cluster/cluster_science_archive/cl_load_csa.pro` sets
`base_url='https://csa.esac.esa.int/csa-sl-tap/data'`, and the code names the interface in its own
words — the header documents `use_tap: If specified, use the newer TAP interface rather than the
default CAIO interface`, and the line immediately above the URL records
`newer TAP system; CAIO method no longer supported JWL 2021-10-08`. The loader serves all four probes
(`master_probes=['C1','C2','C3','C4']`) across 43 named `master_datatypes` spanning CIS, EDI, EFW,
FGM, PEACE, RAPID, STAFF, WBD and WHISPER products.

Two precisions a future refresh needs. **TAP is not optional here**, despite that keyword text:
`use_tap` appears only in the header comments of `cl_load_csa.pro` and `cl_load_csa_crib.pro` and
never as a keyword parameter in the procedure declaration, so the TAP base URL is unconditional and
the CAIO alternative is gone. And **SPEDAS uses the TAP service's product-retrieval path**
(`retrieval_type=PRODUCT&DATASET_ID=...`) rather than its ADQL table-query path, which is exactly why
`ivoa`, `adql`, `votable`, `table access protocol` and `/tap/` return nothing anywhere in the tree:
the endpoint is a TAP service, but SPEDAS never issues an ADQL query and never parses a VOTable.

**`TAP` must not be removed on the strength of a negative keyword search, and two searches make that
mistake inviting.** The first is the IVOA *query* vocabulary above: a product-retrieval client
legitimately never issues ADQL and never parses a VOTable, so that emptiness is not evidence that TAP
is unsupported. The second is a substring search for `tap`, which surfaces the PSP FIELDS
digital-filter-bank terms — `wav_tap`, `d_tap`, `tap_arr` in
`projects/SPP/fields/l1/l1_dfb_wf/spp_fld_dfb_wf_load_l1.pro` and the `ftap` variables in
`projects/SPP/fields/l1/l1_dfb_dbm/spp_fld_dfb_dbm_load_l1.pro`, all signal-processing filter taps.
Those PSP matches are real and genuinely unrelated, but they are not the only ones: a word-boundary
search for `tap` returns four files, and the other two are the Cluster Science Archive pair above.
`TAP` is supported by the 6.1 sources and stays.

**A related negative result worth keeping, because it is easy to mistake for the justification.** The
IUGONET metadata database is *not* a TAP service. `projects/iugonet/tools/mddb/iug_makequery_mddb.pro`
sets `mddb_base_url = 'http://search.iugonet.org/iugonet/open-search/'`, and
`get_source_url_list.pro` documents its input as "Query in the OpenSearch format", parsed by
`iug_parsexml_mddb.pro`. It is the tree's other registry-query interface, it is OpenSearch, it
supports no Data Sources row of its own, and it is not what `TAP` rests on.

**Sources considered and not added, with reasons:**

- `AMDA` — no AMDA/CDPP web-service client. The apparent `AMDA` hits are substring matches inside
  unrelated identifiers.
- `Madrigal` and `VirES` — no occurrence anywhere in the tree.
- `The Virtual Solar Observatory.` — no VSO client: searched for `virtual solar observatory`,
  `vso_search` and `vso.` with no genuine hits. (Noting the trailing period in the row name, which is
  a submission trap, but the value does not apply here regardless.)
- `S3/Cloud-aware` — the tree's only AWS references are three occurrences of one API Gateway REST
  endpoint, `https://mdhkq4bfae.execute-api.eu-west-1.amazonaws.com/prod/science-files-metadata?`, in
  `projects/emm/emm_file_retrieve.pro`, `projects/emm/mvn_emm_crib.pro` and
  `projects/emm/emm_emus_examine_disk.pro`. That is an ordinary HTTPS web service which happens to be
  hosted on AWS. Searching every file in the archive finds no `s3://` URI, no S3 object-store access
  and no cloud-aware chunked reading. `HTTP/HTTPS Directories` already covers the EMM endpoint.
- `Other` — unnecessary; every source found maps to a named row.

`Observatory/Mission-specific` is retained and is well supported: the mission-specific archives and
APIs the tree talks to include the MMS Science Data Center with authenticated login
(`projects/mms/sdc/get_mms_sdc_connection.pro`, `mms_sitl_login.pro`), the ELFIN, ERG, MAVEN, PSP,
GOES/GOES-R, POES and DSCOVR project servers, and ESA's SOSMAG HAPI endpoint. Field 32 lists the
corresponding missions, which is the cross-listing this field's guidance requires.

### 18. Input File Formats (RECOMMENDED)

- ascii
- CDF
- csv
- FITS
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4

Seven values carry over from the existing HSSI record; `HDF5` and `JSON` are additions.

- **HDF5** — `general/hdf/hdf2tplot.pro` states its purpose as "Load HDF-5/netCDF-4 files into tplot"
  and notes "Uses the HDF5 IDL library"; `general/hdf/hdf_to_cdfstruct.pro` calls `h5f_open`,
  `h5d_read`, `h5a_read` and the rest of IDL's HDF5 API directly; and
  `general/missions/rbsp/ect/rbsp_read_ect_mag_ephem.pro` reads the ECT magnetic-ephemeris HDF5 files.
- **JSON** — `general/spedas_tools/hapi/hapi_load_data.pro` parses HAPI responses with
  `table = json_parse(string(neturl->get(/buffer)))`; `projects/sosmag/hapi/sosmag_json_parse.pro` and
  `projects/sosmag/hapi/sosmag_hapi_query.pro` do the same for ESA's HAPI service; `projects/mms/common/load_data/
  mms_parse_json.pro` parses the MMS SDC's JSON responses; and `projects/SWFO/STIS/
  json_reader__define.pro` is a data reader that "works with the common block files to decommutate
  data from Keysight power supplies", translating JSON records into data structures.

Retained values are all supported: `CDF` (`general/CDF/`, 20 top-level routines and 31 including
`obsolete/`), `ISTP-Compliant`
(`general/CDF/spd_cdf2tplot.pro` and the `gatt2istp`/`vatt2istp` ISTP attribute mappings in
`hdf2tplot.pro`), `netCDF3/4` (`general/netCDF/netcdf2tplot.pro`, `projects/icon/load/
icon_netcdf2tplot.pro`, the GOES `.nc` paths), `ascii` (`general/tools/misc/read_asc.pro`,
`general/misc/read_ascii_cmdline.pro`, `projects/secs/sec_read_ascii_data.pro`, `projects/SWFO/STIS/
ascii_reader__define.pro`), `csv` (`projects/sosmag/sosmag_load_csv.pro` with the shipped
`sosmag_test_data.csv`, `projects/mms/sitl/sitl_quick_sample_input.csv`), `IDL.sav`
(`projects/themis/spacecraft/thm_hsk_conversions.sav`, `general/missions/fast/fast_orbit_times.sav`,
`spedas_gui/Resources/spd_ui_*_template.sav` and 89 `.sav` files in total), and `FITS`
(`external/astron/fits/` plus `projects/iugonet/load/iug_ant_fits2tplot.pro`, `iug_load_iprt.pro`,
`iug_load_smart.pro`, `projects/emm/emm_emus_examine_disk.pro`).

Considered and not added: `Zarr` (no occurrence in the tree).

### 19. Output File Formats (RECOMMENDED)

- ascii
- CDF
- csv
- IDL.sav
- ISTP-Compliant
- netCDF3/4
- Other

Six values carry over from the existing HSSI record; `netCDF3/4` is the addition, justified by
`projects/SWFO/STIS/swfo_ncdf_create.pro`, which calls
`ncdf_create(ncdf_filename,/clobber,/netcdf4_format)` and defines dimensions and variables, and by
`swfo_stis_make_l0b.pro` and `swfo_gen_apdat__define.pro`, which produce L0b netCDF products through
it.

Retained values: `CDF` and `ISTP-Compliant` (`general/CDF/tplot2cdf.pro`, `tplot2cdf_save_vars.pro`,
`cdf_save_vars.pro`, `mag_sts_to_cdf.pro`, `projects/maven/mvn_pf_make_cdf.pro`, the RBSP EFW L2/L3
producers, and `projects/themis/spin/spinmodel_python_test.pro` which writes a CDF explicitly for
cross-language comparison); `ascii` (`general/misc/write_ascii.pro`, `write_ascii_cmdline.pro`);
`csv` (the SITL selection and burst-segment tables); `IDL.sav` (`general/tplot/tplot_save.pro` and
`tplot_file.pro`, which save and restore tplot variables as IDL save files);
`Other` (raster and vector graphics output — `general/misc/makepng.pro`, `makegif.pro`, `makejpg.pro`,
`make_jpeg.pro`, `makeps.pro`, `popen.pro`/`pclose.pro` for PostScript, and
`spedas_gui/panels/spd_ui_image_export.pro`).

Considered and not added: `FITS`. The bundled IDL Astronomy User's Library does ship FITS writers
(`external/astron/fits/writefits.pro` and `mwrfits.pro`), so a user with SPEDAS installed can write
FITS — but no SPEDAS routine outside `external/astron/` calls them, so FITS is not an output format
*of this software*. Also not added: `JSON` and `HDF5`. `json_serialize` does appear in active code
(`projects/mms/sitl/bss/mms_bss_table.pro`, `projects/mms/sitl/eva/source/script/
sitl_report_latest_json.pro`), but it writes MMS SITL burst-segment status tables rather than science
data products; recording JSON as a scientific output format would overstate it. That is a judgement
call about where the line falls, and a future refresh could reasonably read it differently. No HDF5
writer exists in the tree.

### 20. Operating System (RECOMMENDED)

- Linux
- Mac
- Solaris
- Windows

Carried over from the existing HSSI record unchanged.

Linux, Mac and Windows are stated by the project: the wiki `Main_Page` says the framework "Works with
Windows, Linux and Mac OS X", and `Downloads_and_Installation` has per-platform installation and
troubleshooting sections for all three ("IDL Installation issues on Mac", "Installation on Windows",
"Known issues on Linux"). The code agrees — `general/spedas_tools/spd_read_current_version.pro` and
many other routines branch on `!version.os_family eq 'windows'`.

**`Solaris` is well supported, and the shape of that support is worth recording.** Two independent
lines. The project's own installation page names Solaris twice: it directs licence-less users to
"Download the SPEDAS save file (for Solaris or other operating systems)", and its `IDL_PATH` setup
instructions say to "place the following in your .bashrc (Linux, Solaris) or .bash_profile (Mac)
file". And the distribution ships `projects/wind/3dp/idl/wind3dp_lib_sunos_sparc.so`, a SunOS/SPARC
build of the Wind 3DP decommutation library, alongside its Linux and macOS siblings. Note the
asymmetry: Solaris is supported through the save-file/VM route and the SPARC binary rather than
through the three-platform executables, which is why `Main_Page`'s summary sentence names only
Windows, Linux and Mac OS X. That summary sentence is not evidence that the project has dropped
Solaris — `Downloads_and_Installation` names it twice, as quoted above — so the value rests on
documentation as well as on a shipped binary.

Considered and not recorded: `Operating System Independent` — SPEDAS's IDL core is platform
independent, but the distribution contains per-platform compiled libraries and the project documents
platform-specific installation issues, so a blanket independence claim would be inaccurate.
(Recording the exact spelling here because `OS Independent` is not a value and would be rejected.)
`MobilePlatform` and `Other` do not apply.

### 21. CPU Architecture (RECOMMENDED)

- CPU Independent
- x86-64
- Sun (SPARC)

The HSSI record previously carried no CPU architecture.

These three are complementary rather than contradictory, and the reason is worth stating plainly. The
5,882-file interpreted IDL core has no CPU-specific requirement — the wiki says SPEDAS "Is based on
IDL, benefiting from platform independence" — which is `CPU Independent`. The distribution also ships
compiled native libraries, and their filenames name the architectures exactly:
`projects/wind/3dp/idl/wind3dp_lib_linux_x86_64.so` and `wind3dp_lib_darwin_x86_64.so` give
`x86-64`; `wind3dp_lib_sunos_sparc.so` gives `Sun (SPARC)`, which is also why `Solaris` appears in
Field 20.

Considered and not recorded, each with its reason:

- `Apple Silicon arm64` and `Linux aarch64 or arm64` — no arm64 build of `wind3dp_lib` is shipped and
  no arm64 artifact appears anywhere in the tree. IDL 8.9 and later run natively on Apple Silicon, so
  the IDL core almost certainly works there, but that is a property of the IDL runtime rather than
  evidence about this distribution. `CPU Independent` already carries the portability claim.
- `ppc64le` — deliberately **not** used for `wind3dp_lib_darwin_ppc.so`. That library is 32-bit
  big-endian PowerPC for classic Mac OS X; `ppc64le` is 64-bit little-endian POWER. They are
  different architectures and the vocabulary has no row for the former.
- 32-bit x86 — `wind3dp_lib_linux_x86.so` and `wind3dp_lib_darwin_i386.so` are shipped, but the
  vocabulary has no 32-bit x86 row (`x86-64` is 64-bit only), so there is nothing to record.
- `GPU`, `HPC or HEC` — no GPU code and no parallel/HPC code (see Field 4's rejected
  `Servers and Environments: High Performance Computing`).
- `Other` — unnecessary; the applicable architectures have rows.

### 22. Related Phenomena (OPTIONAL)

- Geomagnetic Storms
- Solar Wind
- X-ray emission

The HSSI record previously carried no phenomena.

- **Geomagnetic Storms** — the geomagnetic index infrastructure: `general/missions/kyoto/
  kyoto_load_dst.pro` and `kyoto_load_ae.pro` (Kyoto Dst and AE), `general/missions/noaa/
  noaa_load_kp.pro` (Kp), `general/key_param/load_dst.pro`, `general/key_param/load_ig_pci.pro`
  (Polar Cap index), `projects/themis/ground/thm_make_ae.pro` and `thm_load_pseudoae.pro`, and
  `projects/geom_indices/`. Dst, AE and Kp are the standard storm indices, and SPEDAS provides the
  loaders and plotting for them.
- **Solar Wind** — see Field 5's `Solar Wind` evidence: the ACE, Wind, DSCOVR, OMNI and PSP SWEAP
  loaders, plus `external/IDL_GEOPACK/calc_pdyn.pro` and `tcalc_pdyn.pro` which compute solar-wind
  dynamic pressure as a model driver.
- **X-ray emission** — two independent lines. Solar: `projects/goes/goes_load_data.pro` datatype
  `'xrs': X-ray Sensor` for GOES 8–15 and `projects/goesr/goesr_load_data.pro` datatype
  `'xrs': EXIS X-Ray Sensor` for GOES-16/17. Magnetospheric/atmospheric: the BARREL balloon X-ray
  spectrometers, `projects/barrel/barrel_load_{sspc,mspc,fspc}.pro` (slow, medium and fast X-ray
  spectra) with `brl_find511.pro` locating the 511 keV annihilation line and `brl_makebkgd.pro`,
  `brl_makeedges.pro` handling spectral background and channel edges.

**Phenomena considered and not recorded:**

- `Coronal Mass Ejections` — SPEDAS 6.1 has no CME detection, tracking, fitting or catalogue support.
  The coronagraph and heliospheric imagers that CME work depends on (STEREO SECCHI, SOHO LASCO) are
  not supported by any loader in the tree.
- `Solar Flares` — GOES XRS is the canonical flare monitor and SPEDAS loads it, but it provides no
  flare-specific capability: no flare classification, no event list, no flare catalogue query, no
  hard X-ray imaging spectroscopy. The XRS support is fully described by `X-ray emission`, and adding
  `Solar Flares` on the strength of the same loader would double-count it as a capability SPEDAS does
  not have.
- `Solar Corona` and `Coronal Heating` — no coronal imaging, spectroscopy or modelling of any kind.

Noting for a future refresh that this vocabulary is closed and small: `Radiation Belts`,
`Substorms`, `Magnetic Reconnection` and `Aurora` — all central to what SPEDAS supports — have no
rows, and Field 22's own guidance sends such terms to Keywords instead. `radiation belts` and
`aurora` are accordingly in Field 16. `Coronal Holes` is not a value in this vocabulary despite
appearing in older documentation, and would be rejected on submission.

### 23. Development Status (RECOMMENDED)
`Active`

The HSSI record previously carried no development status. repostatus.org defines `Active` as
"Reached stable, usable state and being actively developed", and both halves hold:

*Stable and usable* — 6.1 is a QA-completed general release: the wiki states "The QA process for
SPEDAS 6.1 has now been completed, and this version of the software is now released for general use."

*Actively developed* — a nightly build is produced every day and was current at 2026-08-11 when the
downloads directory was read ("This is built every day and it contains the most recent source code");
the official GitHub mirror was last pushed 2026-08-10; the release cadence produced 6.0 in December
2023 and 6.1 in May/June 2024; and the newest `$LastChangedDate$` keywords inside the 6.1 archive run
to June 2024, consistent with an active trunk at the time the tag was cut.

Considered and rejected: `Inactive` and `Unsupported` (contradicted by daily builds, a monitored
public issue tracker and recent releases); `WIP` and `Concept` (contradicted by a QA-completed general
release with a ten-year release history); `Moved` (the download location has not moved — it is the
same `spedas.org/downloads` directory that still serves every release back to `spedas_1_00.zip`, and
the GitHub mirror explicitly declines to be the authoritative location); `Abandoned` and `Suspended`
(plainly contradicted).

### 24. Documentation (RECOMMENDED)
`https://spedas.org/wiki`

Carried over from the existing HSSI record and confirmed correct. The wiki is the project's
documentation hub and includes installation instructions, which is what this field asks for: its
`Downloads_and_Installation` page covers downloading, unzipping, creating an IDL project,
installing the required CDF and Geopack DLMs, per-platform troubleshooting, and "Running SPEDAS for
the first time". `Main_Page` links the HTML function reference, User's Guide, Developer's Guide and
crib sheets from there. Verified reachable 2026-08-12. No change.

### 25. Funder (OPTIONAL)
`National Aeronautics and Space Administration` — identifier `https://ror.org/027ka1x80`

Carried over from the existing HSSI record and confirmed correct; no change. DataCite's
`fundingReferences` on both the concept and 6.1 DOIs name `National Aeronautics and Space
Administration` with `funderIdentifier` `10.13039/100000104` (Crossref Funder ID) for all three
awards, and `https://ror.org/027ka1x80` is that organization's ROR. Crossref's record for the
reference publication names the same funder for the same award numbers. The name is already the fully
expanded institutional form rather than the acronym, as the field requires.

No other funder is recorded, and the reason needs stating carefully, because one obvious source
appears to contradict it. **The reference publication's Crossref funding block names five funders, not
one:** across 19 award entries it lists the National Aeronautics and Space Administration (7 awards —
`NNG17PZ01C`, `NNG04EB99C`, `NAS5-02099`, `NNX16AP95G`, `NNN06AA01C`, `NNX08AM58G`, `NNX17AL22G`), the
Japan Society for the Promotion of Science (4), the Ministry of Science and Technology, Taiwan (4), the
National Science Foundation (3) and the Deutsches Zentrum für Luft- und Raumfahrt (1).

**The Field 25 value is NASA alone, and the other four Crossref funders are rejected alternatives
rather than omissions.** Two grounds decide it:

- The **software deposit's** own funding metadata names one funder, consistently across every version.
  DataCite's `fundingReferences` on the concept DOI and on all twelve version DOIs list exactly the
  same three awards, all NASA — the three in Field 26. Thirteen independent deposit records agreeing
  on one funder and three awards is the authoritative funding statement for *this software*.
- The four other Crossref funders belong to the paper's co-authors, not to this software. The 2019
  paper has 102 authors drawn from the mission and ground-network teams SPEDAS supports, and its
  funding block is the union of what funded **those authors' contributions to the paper**: the Japan
  Society for the Promotion of Science and Ministry of Science and Technology, Taiwan awards attach to
  the ERG/Arase and IUGONET co-authors, the Deutsches Zentrum für Luft- und Raumfahrt award to a
  German co-author, and the National Science Foundation awards likewise to co-authors' own programmes.
  Reading a 102-author paper's funding block as the funder list of one of the software packages it
  describes would attribute SPEDAS's funding to agencies that funded other people's science.

**So a future refresh should not reintroduce JSPS, MOST Taiwan, NSF or DLR from Crossref.** They are
genuinely present in the reference publication's funding block — that is not an error in Crossref, and
re-finding them there is not new information. Their role is co-author attribution, and the deciding
evidence against promoting them is the unanimity of the thirteen deposit records above. The same
applies to the four additional *NASA* awards in that block (`NNX16AP95G`, `NNN06AA01C`, `NNX08AM58G`,
`NNX17AL22G`), which change no funder value and are addressed in Field 26.

Separately, individual mission plug-ins in the tree are contributed by non-NASA institutions
(ISEE/Nagoya and ISAS/JAXA for ERG, IUGONET for the Japanese ground network, ESA for SOSMAG, the
British Antarctic Survey for its magnetometers), but that is contributed code rather than funding *of
this software*, and no source attributes SPEDAS funding to those agencies.

### 26. Award Title (OPTIONAL)

| Award title | Award number |
|---|---|
| MMS | NNG04EB99C |
| SPEDAS Community Support | NNG17PZ01C |
| THEMIS | NAS5-02099 |

Carried over from the existing HSSI record and confirmed correct; no change. All three match
DataCite's `fundingReferences` on the 6.1 DOI exactly, both title and number, and match the concept
DOI's three entries as well. Crossref's funding block for the reference publication independently
lists all three numbers — `NNG17PZ01C`, `NNG04EB99C` and `NAS5-02099` — under NASA, among the four
further NASA awards and four other funders discussed in Field 25.

The award *titles* are the project's own short mission-programme labels rather than formal grant
titles; they are recorded as DataCite states them, because DataCite is the authoritative deposit
metadata and inventing longer titles would be fabrication.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found — no defensible entries.

**HSSI stored an empty list, and after research it should stay empty.** This is a documented negative
result, not an unfinished search.

Field 27 asks for publications "the software developer prioritizes but are different from the
reference publication". The project prioritizes exactly one paper, and it is already Field 14: the
wiki's "Citing SPEDAS" section names only `10.1007/s11214-018-0576-4`, and DataCite records exactly
one `IsDescribedBy` relation, to that same DOI. Duplicating it here would misrepresent the record.

What the wiki's "Publications" section actually offers is a single link, "2018 Publications" →
`https://www.spedas.org/papers/SPEDAS_18.html` — a bibliography page of refereed papers that *used*
SPEDAS as an analysis tool. It is a list of third-party citing works with no DOI of its own, not a
publication the developers prioritize, and enumerating a citing bibliography into this field would
add hundreds of entries that say nothing about the software.

Also considered and rejected: the "Information on the coordinate transformation library Rocotlib and
on a method for computing wave polarization" link under the wiki's External Resources, which resolves
to `https://www.lpp.polytechnique.fr/IMG/pdf/1993_robert_dtcrpe1231_rocotlib.pdf` — a 1993 technical
report, with no DOI, cited as background for the `general/science/wavpol/` method rather than as a
publication about SPEDAS. Also rejected: the SPEDAS release-notes documents linked from the wiki,
which are project PDFs without DOIs. The twelve Zenodo *version* DOIs are software, not
publications, and belong to Fields 2 and 12.

### 28. Related Datasets (OPTIONAL)

Three datasets, all World Data Center for Geomagnetism, Kyoto geomagnetic indices.

| Dataset | DOI | Where SPEDAS states it |
|---|---|---|
| WDC Kyoto Dst index | `https://doi.org/10.17593/14515-74000` | `projects/iugonet/load/iug_load_gmag_wdc_create_tplot_vars.pro`, `acknowledg_str_dst`: "Please cite the data DOI (10.17593/14515-74000) when using the index in your paper." |
| WDC Kyoto AE index | `https://doi.org/10.17593/15031-54800` | the same file, `acknowledg_str_ae` |
| WDC Kyoto Wp index | `https://doi.org/10.17593/13437-46800` | `projects/iugonet/load/iug_load_gmag_wdc_wp_index.pro`: "it is highly recommended to cite the above paper and data DOI (doi:10.17593/13437-46800)." |

**HSSI stored an empty list; these three are additions, and the selection principle is what makes them
defensible.** SPEDAS supports thousands of datasets across roughly fifty missions and ground networks,
so the field's real difficulty is not finding dataset DOIs but justifying a bound. These three are
bounded by the software's own behaviour: they are the datasets whose DOIs **SPEDAS itself names and
instructs its users to cite**, in acknowledgement text the loaders attach to the tplot variables they
create. That is the software speaking about specific data products it has purpose-built loaders for
(`general/missions/kyoto/kyoto_load_dst.pro`, `kyoto_load_ae.pro`, and the
`projects/iugonet/load/iug_load_gmag_wdc*.pro` family), not a passing citation in a header comment.

**Why the field stops at three rather than growing toward SPEDAS's whole catalogue.** Beyond these,
any selection would be arbitrary — nothing would justify picking, say, the MMS FPI burst product over
the THEMIS FGM product — and listing everything would be an unbounded catalogue. The dataset-level
relationships SPEDAS actually has are carried by Fields 31 and 32 at instrument and observatory
granularity, and by Field 17 for the archives the data comes from. A future refresh that wanted true
dataset granularity has a concrete route: every mission loader's remote path corresponds to a SPASE
`NumericalData` product with an `hpde.io` identifier (the form the field's own example uses), so the
list could be derived from the loaders — but it would be very large and should be a deliberate
decision rather than a side effect of extraction.

**Registration facts, so the DOIs are not mistaken for broken ones.** All three are registered through
JaLC (the Japan Link Center) rather than DataCite: `https://doi.org/doiRA/<doi>` returns `"RA": "JaLC"`
for each, and each resolves to NICT Japan's data-DOI service at
`https://isds-datadoi.nict.go.jp/wds/...`. The DataCite API accordingly returns 404 for all three,
which is expected for a non-DataCite registrant and is **not** a sign the DOIs are invalid.
Content-negotiated citation metadata confirms them: `"publisher": "WDC for Geomagnetism, Kyoto"` with
titles `Dst Index`, `AE Index` and `Wp Index`.

**The surrounding DOI census, so these three are not mistaken for all the DOIs in the tree — or for
none of them.** Counted over every file in the archive, 49 files carry a DOI-like string and they hold
**38 distinct DOIs**; the figure drops to 32 if the count is restricted to `.pro` files, which is a
narrower basis than the 49-file figure and is the easy way to undercount. All but these three carry
journal publisher prefixes (`10.1002`, `10.1007`, `10.1016`, `10.1029`, `10.1038`, `10.1109`,
`10.1209`, `10.3847`, `10.5194`) and are method references in routine headers rather than data
products.

**No SPEDAS DOI asserts a dataset relation, which is why the deposit metadata could not supply this
field.** Checked on the concept DOI and on each of the twelve version DOIs: the only relation types
present are `IsDescribedBy` (to the reference publication), `IsSupplementTo` (to the PySPEDAS
repository) and `IsVersionOf`/`HasVersion`. There is also no `CITATION`-style dataset manifest anywhere
in the archive. The three values above rest entirely on the loaders' own acknowledgement text.

### 29. Related Software (OPTIONAL)

| Software | Link |
|---|---|
| PySPEDAS | https://github.com/spedas/pyspedas |
| IDL Geopack (Tsyganenko model wrapper) | http://ampere.jhuapl.edu/code/idl_geopack.html |
| das2dlm | https://github.com/das-developers/das2dlm |
| IDL ICY (NAIF SPICE toolkit for IDL) | https://naif.jpl.nasa.gov/naif/toolkit_IDL.html |
| NASA CDF library | https://cdf.gsfc.nasa.gov/ |
| IDL Astronomy User's Library | https://idlastro.gsfc.nasa.gov/ |

The HSSI record previously carried no related software. Each entry is either a predecessor/companion
implementation or a *domain-specific* dependency the project itself requires users to install; none
would be equally true of an arbitrary package.

- **PySPEDAS** is the Python implementation of this software — the same project, same organization,
  different language. DataCite records `IsSupplementTo https://github.com/spedas/pyspedas` on both
  SPEDAS DOIs; the wiki devotes a "Python" section and a "Looking for PySPEDAS?" banner to it. It is
  the single most informative thing one can say about this record's scope, because it is what
  distinguishes the IDL framework from its Python counterpart. Recorded with the repository URL
  because that is the identifier DataCite itself asserts.
- **IDL Geopack** is a required separate install, not a bundled convenience.
  `external/IDL_GEOPACK/README.txt`: "To use the functions external/IDL_GEOPACK you will need to
  install Haje Korth's IDL wrapper for N.A. Tsyganenko's magnetic fields model package… Download the
  IDL geopack for your architecture from: http://ampere.jhuapl.edu/code/idl_geopack.html", then copy
  `idl_geopack.dlm` and its binary into IDL's DLM directory. The wiki `Downloads_and_Installation`
  lists it under "IDL libraries". Every value in Field 4's `Models and Simulations: Empirical` and
  both `Field-line Tracing` entries depends on it.
- **das2dlm** provides the das2 protocol client. `external/das2dlm/` holds the IDL-side wrappers
  (`das2dlm_get_ds_var.pro`, `das2dlm_add_metadata.pro`, the time converters) while the compiled DLM
  is a separate install the wiki lists as "IDL DAS2 Library". It is what makes Field 17's `das2`
  value and the Cassini and Juno support possible.
- **IDL ICY** is NAIF/JPL's IDL wrapper for SPICE, again a required separate install.
  `external/IDL_ICY/README.txt`: "you will need to install NAIF/JPL's IDL wrapper for SPICE… Download
  the icy.zip or icy.tar.Z file for your architecture from: http://naif.jpl.nasa.gov/naif/
  toolkit_IDL.html", then install `icy.dlm`. All of `general/spice/` — and with it Field 4's
  `Coordinate Transforms: Mission-Specific`, `Planetary` and `Heliospheric` — depends on it.
- **NASA CDF library.** The wiki instructs: "You may also need to separately download and install the
  latest CDF DLM from NASA". CDF is the heliophysics community's data format, produced and maintained
  by NASA/GSFC — not general-purpose I/O plumbing — and `general/CDF/`'s 20 top-level routines are the
  backbone
  of both Field 18 and Field 19.
- **IDL Astronomy User's Library** ships bundled as `external/astron/` (`fits/`, `fits_bintable/`,
  `fits_misc/`, `fits_table/`) and is what provides Field 18's `FITS` support;
  `external/astron/fits/readfits.pro` points at `http://idlastro.gsfc.nasa.gov/fitsio.html`. It is an
  astronomy-specific library, not generic infrastructure.

**Considered and deliberately excluded:**

- **mgunit** (Michael Galloy's IDL unit-test framework, bundled at `general/qa_tools/mgunit/` and
  `projects/mms/sdc/test_tools/mgunit.sav`) — generic testing infrastructure. It would be equally at
  home in any IDL project of any discipline, so it carries no information about this software.
- **SolarSoft** — `general/misc/SSW/` looks like a SolarSoft dependency but is not: it is 21 borrowed
  general-purpose utility routines (`bsort.pro`, `dprint.pro`, `tag_exist.pro`, `is_string.pro`,
  `str_replace` variants). SolarSoft itself is neither bundled nor required, and no SPEDAS routine
  calls into a SolarSoft installation. Recording it would assert a dependency relationship that does
  not exist.
- **AACGM-v2** (`external/aacgm_v2/`) — a genuine domain-specific bundled component and a reasonable
  candidate, held back only because it has no stable canonical project URL or DOI to record, and the
  field requires a link. Named here so a future refresh can add it if one is found.
- **Autoplot** — a peer space-physics tool and arguably a Field 29 entry too, but its relationship
  here is a demonstrated bidirectional data exchange, so it is recorded in Field 30 rather than
  duplicated.
- **Rocotlib** — background for the wave-polarization method, available only as a 1993 technical
  report PDF rather than as obtainable software (see Field 27).
- **IDL itself** — the runtime, not related software; its commercial-licence implication is recorded
  under Field 15.

### 30. Interoperable Software (OPTIONAL)

| Software | Link |
|---|---|
| PySPEDAS | https://github.com/spedas/pyspedas |
| PyTplot | https://github.com/MAVENSDC/PyTplot |
| Autoplot | https://autoplot.org/ |

The HSSI record previously carried no interoperable software. Each entry rests on a specific
demonstrated exchange in the shipped code, not on co-presence or ecosystem membership.

- **PySPEDAS.** `general/spedas_tools/python_validation/spd_run_py_validation.pro` "Runs a Python
  script and checks that tplot variables match those currently loaded in IDL", comparing values to a
  numeric `tolerance`. The scripts it runs are PySPEDAS:
  `general/spedas_tools/python_validation/general_validation_ut__define.pro` builds
  `["from pytplot import tplot_rename", "import pyspedas", "variables = pyspedas.omni.data(...)"]`;
  `projects/mms/common/tests/mms_python_validation_ut__define.pro` drives `pyspedas.mms.fpi`,
  `pyspedas.mms.fgm`, `pyspedas.mms.lingradest` and `mms_feeps_gpd`;
  `projects/themis/common/tests/thm_python_validation_ut__define.pro` does the same for THEMIS. The
  exchange runs the other way too: `projects/themis/spin/spinmodel_python_test.pro` exports THEMIS
  spin models "as CDFs for comparison with Python results", producing "a CDF … to be reproduced in
  pyspedas" and naming the Python-side entry point `themis.state.spinmodel.validate_model`. The two
  packages share the tplot variable model, which is exactly the shared-data-model criterion.
- **PyTplot** is the Python side of that shared model and is imported directly by the harness —
  `from pytplot import store_data` in `py_validation_example_ut__define.pro` and
  `from pytplot import tplot_rename` in `general_validation_ut__define.pro` — so SPEDAS's own tests
  write into and rename PyTplot variables.
- **Autoplot.** `general/spedas_tools/tplot2ap/tplot2ap.pro` has the documented purpose "Send tplot
  variables to Autoplot", connecting to "Autoplot server port (default: 12345)" and transferring the
  data as a CDF file; `ap2tplot.pro` is the reverse — "Loads the data from the current Autoplot window
  into tplot variables". Both document the prerequisite ("you'll need to open Autoplot and enable the
  'Server' feature via the 'Options' menu"), which is a concrete, bidirectional, cross-language
  bridge to a named domain tool. `ap2tplot.pro`'s header calls itself "very experimental"; the
  exchange is nonetheless implemented and documented, and the caveat is recorded here so a reader
  knows its maturity.

**Considered and excluded:**

- **The bundled IDL libraries** (IDL Geopack, das2dlm, IDL ICY, NASA CDF, IDL Astronomy User's
  Library, AACGM-v2, mgunit). These are dependencies SPEDAS calls, not peer tools it exchanges data
  with. Being a dependency is not interoperability. The domain-specific ones are in Field 29.
- **Any blanket "part of the heliophysics software ecosystem" claim.** It would read identically for
  most records in HSSI and carries no information.
- **IDL / NV5 IDL** — the runtime environment, not an interoperating peer.
- **Jupyter, xarray, astropy and similar** — genuinely absent. `astropy` and `jupyter` do not occur
  in any `.pro` file; every apparent `xarray` hit is a substring of an ordinary IDL identifier
  (`indexArray`, `fxarray`), and every `notebook` hit is a reference to a co-author's paper lab
  notebook in `projects/maven/lpw/mvn_lpw_prd_lp_n_t_compare_waves.pro`.
- **MATLAB — excluded, and not because the tree is MATLAB-free.** A MAT-file
  reader *is* shipped: `general/misc/load_mat.pro`, whose purpose line is "Read MATLAB MAT-files in
  IDL (see README for more information)". It still fails the Field 30 bar, on three specific grounds:
  no routine anywhere in the tree calls it; it does not produce tplot variables, so no exchange with
  SPEDAS's data model exists; and its docstring is an unfilled template pointing at a README that is
  not present in the archive. It is an orphaned bundled utility, not an interoperability relationship.
  (`projects/poes/poes_contamination_removal.pro` is likewise not a bridge — its header records that
  it was "written by Wen Li based on Drew Turner's matlab code", which is a port.) Recorded so a
  future refresh neither re-proposes MATLAB on the strength of `load_mat.pro` nor concludes from its
  exclusion here that nothing MATLAB-related is in the tree. Note also that the `FileFormat`
  vocabulary has no MAT-file row, so nothing follows for Field 18 either.

### 31. Related Instruments (OPTIONAL)

275 instrument associations. **HSSI stored an empty list**, so all 275 are additions.

**Bounding rule — read this before extending the list.** SPEDAS is a multi-mission framework whose
*true* instrument extent is far larger than any list a single record can carry, so this set is
bounded by a stated rule rather than being exhaustive, and the excluded families are named below so
a later refresh can widen it deliberately. An instrument is recorded only when **all** of the
following hold:

1. SPEDAS 6.1 contains a **dedicated, instrument-specific** loader, calibrator or processor for it —
   not merely a generic CDF/netCDF reader that could ingest its files.
2. The controlled vocabulary has a `type = 1` row for it whose `identifier` begins
   `https://spase-metadata.org/`, and the `name` recorded below is that row's name byte-for-byte.
3. Resolution is unambiguous for that physical entity after three normalizations:
   `.html` identifiers are treated as the same resource as their bare form and the bare form is
   preferred; where an agency-catalogue mirror (`CNES/Instrument/CDPP-AMDA/...`,
   `CNES/Instrument/CDPP-Archive/...`, `NASA/Instrument/...`) describes the same physical instrument
   as an `SMWG/Instrument/...` row, the SMWG row is preferred as the canonical registry entry — but
   that is a *tie-breaker*, so where an instrument has only an agency-catalogue row and no SMWG
   counterpart, the single agency row is the correct value (this is what licenses the two ELFIN EPD
   rows below, on the same footing as `ESA/Observatory/SolarOrbiter`); and a name shared by
   *different* entities (four `MMS FIELDS/FGM` rows, one per probe) is not a collision, whereas two
   SMWG rows for the *same* entity is.
4. The spacecraft is named by an explicit in-tree supported-spacecraft list or by a per-spacecraft
   loader, which is what licenses the per-probe expansion.

Per-spacecraft expansion evidence, mission by mission:
`projects/themis/spacecraft/fields/thm_load_fgm.pro` line 286 sets `vsnames = 'a b c d e'`;
twelve of the 74 `mms_load_*.pro` routines state "valid values for MMS probes are ['1','2','3','4']"
in their headers, and they are exactly the twelve instrument loaders whose SPASE rows are recorded
below — `projects/mms/{aspoc,dsp,edi,edp,eis,feeps,fgm,fpi,fsm,hpca,mec,scm}/mms_load_*.pro`, one per
instrument directory. The other 62 `mms_load_*.pro` files are not instrument loaders and so do not
carry the sentence: 17 are `*_ut__define.pro` test objects, 25 are example cribs and quicklook scripts,
and the remaining 20 are the shared dispatcher `common/load_data/mms_load_data.pro` and its SPDF
sibling, burst/fast/SROI segment-status helpers, the SITL burst-selection loaders under `sitl/bss/`,
the ASCII ephemeris/attitude readers under `mec_ascii/` (including `mms_load_state.pro`), and
per-datatype post-processors such as `fpi/mms_load_fpi_calc_pad.pro`. Independently,
`projects/mms/particles/mms_part_getspec.pro` hard-codes `probes = ['1', '2', '3', '4']`;
`projects/cluster/` has one directory per instrument (`aspoc cis dwp edi efw fgm peace rapid staff
wbd whisper`) plus `cluster_science_archive/` for all four spacecraft;
`general/missions/rbsp/` carries per-probe A/B paths throughout;
`general/missions/stereo/st_mag_load.pro` computes `probes = (['a','b'])[pn]` and
`dir = (['ahead','behind'])[pn]`;
`projects/goes/goes_load_data.pro` states "flux-gate magnetometer -- valid for GOES 08-15" and rejects
probes 16/17 with "This routine is only valid for GOES-N data";
`projects/goesr/goesr_load_data.pro` states "Loads data from GOES-R satelites (GOES-16, GOES-17)".

Per-instrument loader evidence, mission by mission:
**THEMIS** — `thm_load_fgm`/`thm_cal_fgm`, `thm_load_efi`/`thm_cal_efi`, `thm_load_scm`/`thm_cal_scm`,
`thm_load_esa` with the `peef`/`peeb`/`peer`/`peif`/`peib`/`peir` family,
`particles/SST/thm_load_sst.pro`, `thm_load_mom`/`thm_cal_mom`, `thm_load_fbk`/`thm_cal_fbk`,
`thm_load_state`/`thm_load_slp`.
**MMS** — `mms_load_{fgm,scm,edp,dsp,edi,fpi,hpca,eis,feeps,aspoc,mec,fsm,state}.pro`; `edp` covers
both the Spin-plane and Axial Double Probes, which is why `FIELDS/SDP` and `FIELDS/ADP` are both
recorded, and `mec`/`state` justify `Ephemeris`.
**Cluster** — the eleven instrument directories above.
**RBSP** — `rbsp_load_ect_l3`, `rbsp_load_mageis_l2`, `rbsp_load_efw_*` (eleven routines),
`rbsp_load_emfisis*`, `rbsp_load_rbspice*`, `rbsp_load_spice_cdf_file`, `rbsp_read_ect_mag_ephem`.
**PSP** — `projects/SPP/fields/` (`psp_load_mag`, `psp_load_scm`, `psp_load_dfb_{ac,dc}_spec`,
`psp_load_rfs`/`psp_load_rfs_lfr`, `spp_fld_dfb_wf_load_l1` for TDS-adjacent waveforms),
`projects/SPP/sweap/{SPC,SPAN,SWEM}/`, `projects/SPP/isois/spp_isois_load.pro`,
`spp_fld_ephem_*_load_l1`.
**MAVEN** — `projects/maven/{mag,swea,swia,sta,sep,lpw,euv,ngi,iuvs,eph}/`, one per SPASE row.
**Wind** — `load_wi_3dp` with the full `projects/wind/3dp/` package, `load_wi_mfi`/`load_wi_h0_mfi`/
`load_wi_sp_mfi`, `load_wi_swe`, `load_wi_wav`, `load_wi_epa`, `load_wi_or`.
**ACE** — `load_ace_{mag,swepam,epam,sis,cris,uleis,sepica}.pro`, which
`load_ace_mag.pro` documents as "Modified by D. Larson 5/2008 to automatically download files from
the ACE data center", setting `source.remote_data_dir = 'http://www.srl.caltech.edu/ACE/ASC/DATA/'`.
**FAST** — `general/missions/fast/{fa_esa,fa_fields,fa_mag,fa_teams,fa_k0}/` and the orbit routines.
**Geotail** — `projects/geotail/geotail_load_data.pro`, whose datatypes are exactly
`'lep', 'mgf', 'orbit'`, plus `general/key_param/load_ge_mgf.pro`.
**ICON** — `projects/icon/load/icon_load_data.pro`, which branches on `'fuv'`, `'ivm'`, `'euv'` and
`'mighti-a'`/`'mighti-b'`.
**DSCOVR** — `projects/dscovr/load/dsc_load_fc.pro` (Faraday Cup), `dsc_load_mag.pro` (Fluxgate
Magnetometer), `dsc_load_or.pro` and `dsc_load_att.pro` (Ephemeris).
**STEREO** — `st_mag_load`/`st_mag_cal` (IMPACT/MAG), `st_swea_load`/`st_swea_dist`/
`st_swea_convert_units` (IMPACT/SWEA), `st_ste_load` (IMPACT/STE), `st_plastic_load` (PLASTIC),
`st_swaves_load` (SWAVES), `st_position_load` (Ephemeris); the IMPACT suite row is recorded alongside
its three supported sub-instruments.
**Mars Express / Venus Express** — `projects/mex/aspera/mex_asp_els_load.pro` and
`mex_asp_ima_load.pro` with their calibration chains; `projects/vex/aspera/vex_asp_els_load.pro` and
`vex_asp_ima_load.pro`.
**Akebono** — `projects/akebono/pws/akb_load_pws.pro`, `rdm/akb_load_rdm.pro`,
`orb/akb_load_orb.pro`.
**ELFIN** — `projects/elfin/load_data/elf_load_epd.pro` for the Energetic Particle Detectors, whose
header declares "valid values for elf probes are ['a','b']" and whose default datatype set
`['pef','pif','pes','pis']` covers the electron (EPDE) and ion (EPDI) fast and survey products, backed
by the calibration chain `projects/elfin/cal_data/{elf_cal_epd,elf_get_epd_calibration,
elf_read_epd_calfile,elf_convert_epd_mv2eng}.pro`, the L1/L2 processors
`projects/elfin/load_data/{elf_epd_l1_postproc,elf_epd_l2_postproc,elf_create_epd_all,
elf_create_l2_epd_cdf,run_epd_l2_processing}.pro`, the overview plotters
`projects/elfin/plots/{epde_plot_overviews,epdi_plot_overviews,
epde_plot_wigrf_multispec_overviews}.pro` and the test suite
`projects/elfin/tests/elf_epd_load_cltestsuite.pro` (23 EPD-named files in all); plus
`elf_load_state.pro` and `elf_load_att.pro` for the state/position products. Both EPD and Ephemeris
resolve; FGM and MRMa/MRMi do not (see the omissions below).
**Cassini** — `projects/cassini/das2dlm_load_cassini_mag_{dc11,ec,mag,vec}.pro`,
`das2dlm_load_cassini_rpws_{gain,specrta,survey,waveform}.pro`,
`das2dlm_load_cassini_ephemeris.pro`. These are ordinary loaders, not example cribs.
**GOES** — `goes_load_data.pro` datatypes `'fgm'` → `MAG`, `'epead'`/`'maged'`/`'magpd'`/`'hepad'`
→ the `SEM` suite row, `'eps'` → `EPS` (GOES 13–15), `'xrs'` → `XRS` (GOES 13–15), with `/noephem`
implying ephemeris is loaded by default; `goesr_load_data.pro` datatype `'mag'` → `MAG` for
GOES-16/17 plus ephemeris.
**POES** — `projects/poes/poes_load_data.pro`, whose remote path is
`/noaa/<probe>/sem2_fluxes-2sec/...` and whose datatypes are the TED and MEPED products of the SEM-2
suite; the probes it names are `['noaa18','noaa19','metop2']`, of which NOAA-18 and NOAA-19 resolve
cleanly.
**SOHO / IMP-8** — `general/key_param/load_so_{cel,cst,ern}.pro` (CELIAS, COSTEP, ERNE) and
`load_i8_{mag,pla}.pro`. These are 1999-vintage ISTP key-parameter readers that expect a locally
staged master index file (`masterfile = 'so_k0_cel_files'`) rather than a configured remote source,
and neither mission appears in the wiki's supported-missions list. They are recorded because the
dedicated per-instrument routines are genuinely present and shipped, but a reader should know the
support is legacy.
**OMNI** — `projects/omni/omni_load_data.pro`; among `SMWG` rows the vocabulary models OMNI's merged
solar-wind product as a single `SMWG/Instrument/OMNI` row (a `CNES/Instrument/CDPP-AMDA/OMNI` mirror
also exists under a different name and is not recorded, per the agency-mirror rule).
**SECS** — `projects/secs/`, the full Spherical Elementary Current Systems plug-in; see the entry
below for why the instrument-level row applies.
**Polar** — `general/key_param/load_po_pwi.pro`, a dedicated Polar Plasma Wave Instrument key-parameter
loader from the same legacy ISTP family as the SOHO and IMP-8 routines.

**THEMIS — 40 rows**

- `THEMIS-A Electric Field Instrument` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/EFI`
- `THEMIS-A Electrostatic Analyzers` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/ESA`
- `THEMIS-A Probe Status` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/Ephemeris`
- `THEMIS-A Digital Fields Board, Filter Bank` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/FBK`
- `THEMIS-A Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/FGM`
- `THEMIS-A:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature.` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/MOM`
- `THEMIS-A: Search Coil Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/SCM`
- `THEMIS-A:  Solid State Telescope` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/A/SST`
- `THEMIS-B Electric Field Instrument` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/EFI`
- `THEMIS-B Electrostatic Analyzers` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/ESA`
- `THEMIS-B Probe Status` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/Ephemeris`
- `THEMIS-B Digital Fields Board, Filter Bank` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/FBK`
- `THEMIS-B Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/FGM`
- `THEMIS-B:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature.` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/MOM`
- `THEMIS-B: Search Coil Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/SCM`
- `THEMIS-B:  Solid State Telescope` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/B/SST`
- `THEMIS-C Electric Field Instrument` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/EFI`
- `THEMIS-C Electrostatic Analyzers` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/ESA`
- `THEMIS-C Probe Status` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/Ephemeris`
- `THEMIS-C Digital Fields Board, Filter Bank` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/FBK`
- `THEMIS-C Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/FGM`
- `THEMIS-C:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature.` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/MOM`
- `THEMIS-C: Search Coil Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/SCM`
- `THEMIS-C:  Solid State Telescope` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/C/SST`
- `THEMIS-D Electric Field Instrument` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/EFI`
- `THEMIS-D Electrostatic Analyzers` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/ESA`
- `THEMIS-D Probe Status` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/Ephemeris`
- `THEMIS-D Digital Fields Board, Filter Bank` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/FBK`
- `THEMIS-D Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/FGM`
- `THEMIS-D:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature.` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/MOM`
- `THEMIS-D: Search Coil Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/SCM`
- `THEMIS-D:  Solid State Telescope` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/D/SST`
- `THEMIS-E Electric Field Instrument` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/EFI`
- `THEMIS-E Electrostatic Analyzers` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/ESA`
- `THEMIS-E Probe Status` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/Ephemeris`
- `THEMIS-E Digital Fields Board, Filter Bank` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/FBK`
- `THEMIS-E Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/FGM`
- `THEMIS-E:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature.` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/MOM`
- `THEMIS-E: Search Coil Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/SCM`
- `THEMIS-E:  Solid State Telescope` — `https://spase-metadata.org/SMWG/Instrument/THEMIS/E/SST`

**MMS — 52 rows**

- `MMS EIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/EIS`
- `MMS FEEPS` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/FEEPS`
- `MMS Positions` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/Ephemeris`
- `MMS 1 FIELDS Suite, Axial Double Probe` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/ADP`
- `MMS FIELDS/DSP` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/DSP`
- `MMS FIELDS/EDI` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/EDI`
- `MMS FIELDS/FGM` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM`
- `MMS FIELDS/SCM` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SCM`
- `MMS FIELDS/SDP` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SDP`
- `MMS FPI/DES` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DES`
- `MMS FPI/DIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS`
- `MMS HPCA` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/HotPlasmaCompositionAnalyzer`
- `MMS ASPOC` — `https://spase-metadata.org/SMWG/Instrument/MMS/1/InstrumentControl/ASPOC`
- `MMS EIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/EIS`
- `MMS FEEPS` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/FEEPS`
- `MMS Positions` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/Ephemeris`
- `MMS 2 FIELDS Suite, Axial Double Probe` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/ADP`
- `MMS FIELDS/DSP` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/DSP`
- `MMS FIELDS/EDI` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/EDI`
- `MMS FIELDS/FGM` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM`
- `MMS FIELDS/SCM` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SCM`
- `MMS FIELDS/SDP` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SDP`
- `MMS FPI/DES` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DES`
- `MMS FPI/DIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS`
- `MMS HPCA` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/HotPlasmaCompositionAnalyzer`
- `MMS ASPOC` — `https://spase-metadata.org/SMWG/Instrument/MMS/2/InstrumentControl/ASPOC`
- `MMS EIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/EIS`
- `MMS FEEPS` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/FEEPS`
- `MMS Positions` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/Ephemeris`
- `MMS 3 FIELDS Suite, Axial Double Probe` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/ADP`
- `MMS FIELDS/DSP` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/DSP`
- `MMS FIELDS/EDI` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/EDI`
- `MMS FIELDS/FGM` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM`
- `MMS FIELDS/SCM` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SCM`
- `MMS FIELDS/SDP` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SDP`
- `MMS FPI/DES` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DES`
- `MMS FPI/DIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS`
- `MMS HPCA` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/HotPlasmaCompositionAnalyzer`
- `MMS ASPOC` — `https://spase-metadata.org/SMWG/Instrument/MMS/3/InstrumentControl/ASPOC`
- `MMS EIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/EIS`
- `MMS FEEPS` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/FEEPS`
- `MMS Positions` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/Ephemeris`
- `MMS 4 FIELDS Suite, Axial Double Probe` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/ADP`
- `MMS FIELDS/DSP` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/DSP`
- `MMS FIELDS/EDI` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/EDI`
- `MMS FIELDS/FGM` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM`
- `MMS FIELDS/SCM` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SCM`
- `MMS FIELDS/SDP` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SDP`
- `MMS FPI/DES` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DES`
- `MMS FPI/DIS` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS`
- `MMS HPCA` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/HotPlasmaCompositionAnalyzer`
- `MMS ASPOC` — `https://spase-metadata.org/SMWG/Instrument/MMS/4/InstrumentControl/ASPOC`

**Cluster — 44 rows**

- `Active Spacecraft Potential Control` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/ASPOC`
- `Cluster Ion Spectrometry` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/CIS`
- `Digital Wave Processor` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/DWP`
- `Electron Drift Instrument` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/EDI`
- `Electric Field and Waves` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/EFW`
- `Cluster-Rumba Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/Ephemeris`
- `Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/FGM`
- `Plasma Electron and Current Experiment` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/PEACE`
- `Research with Adaptive Particle Imaging Detectors` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/RAPID`
- `Spatio-Temporal Analysis of Magnetic Field Fluctuations` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/STAFF`
- `Waves of HF and Sounder for Probing Electron Density by Relaxation` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/WHISPER`
- `Active Spacecraft Potential Control` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/ASPOC`
- `Cluster Ion Spectrometry` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/CIS`
- `Digital Wave Processor` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/DWP`
- `Electron Drift Instrument` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/EDI`
- `Electric Field and Waves` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/EFW`
- `Cluster-Salsa Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/Ephemeris`
- `Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/FGM`
- `Plasma Electron and Current Experiment` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/PEACE`
- `Research with Adaptive Particle Imaging Detectors` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/RAPID`
- `Spatio-Temporal Analysis of Magnetic Field Fluctuations` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/STAFF`
- `Waves of HF and Sounder for Probing Electron Density by Relaxation` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/WHISPER`
- `Active Spacecraft Potential Control` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/ASPOC`
- `Cluster Ion Spectrometry` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/CIS`
- `Digital Wave Processor` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/DWP`
- `Electron Drift Instrument` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/EDI`
- `Electric Field and Waves` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/EFW`
- `Cluster-Samba Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/Ephemeris`
- `Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/FGM`
- `Plasma Electron and Current Experiment` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/PEACE`
- `Research with Adaptive Particle Imaging Detectors` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/RAPID`
- `Spatio-Temporal Analysis of Magnetic Field Fluctuations` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/STAFF`
- `Waves of HF and Sounder for Probing Electron Density by Relaxation` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/WHISPER`
- `Active Spacecraft Potential Control` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/ASPOC`
- `Cluster Ion Spectrometry` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/CIS`
- `Digital Wave Processor` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/DWP`
- `Electron Drift Instrument` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/EDI`
- `Electric Field and Waves` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/EFW`
- `Cluster-Tango Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/Ephemeris`
- `Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/FGM`
- `Plasma Electron and Current Experiment` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/PEACE`
- `Research with Adaptive Particle Imaging Detectors` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/RAPID`
- `Spatio-Temporal Analysis of Magnetic Field Fluctuations` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/STAFF`
- `Waves of HF and Sounder for Probing Electron Density by Relaxation` — `https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/WHISPER`

**RBSP — 10 rows**

- `RBSP ECT` — `https://spase-metadata.org/SMWG/Instrument/RBSP/A/ECT`
- `RBSP EFW` — `https://spase-metadata.org/SMWG/Instrument/RBSP/A/EFW`
- `RBSP EMFISIS` — `https://spase-metadata.org/SMWG/Instrument/RBSP/A/EMFISIS`
- `RBSP Positions` — `https://spase-metadata.org/SMWG/Instrument/RBSP/A/Ephemeris`
- `RBSP RBSPICE` — `https://spase-metadata.org/SMWG/Instrument/RBSP/A/RBSPICE`
- `RBSP ECT` — `https://spase-metadata.org/SMWG/Instrument/RBSP/B/ECT`
- `RBSP EFW` — `https://spase-metadata.org/SMWG/Instrument/RBSP/B/EFW`
- `RBSP EMFISIS` — `https://spase-metadata.org/SMWG/Instrument/RBSP/B/EMFISIS`
- `RBSP Positions` — `https://spase-metadata.org/SMWG/Instrument/RBSP/B/Ephemeris`
- `RBSP RBSPICE` — `https://spase-metadata.org/SMWG/Instrument/RBSP/B/RBSPICE`

**ParkerSolarProbe — 17 rows**

- `PSP Spacecraft Ephemeris Instrument` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/Ephemeris`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/DFB`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/MAG`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/RFS/HFR`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/RFS/LFR`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/SCM`
- `PSP FIELDS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/FIELDS2/TDS`
- `PSP Integrated Science Investigation of the Sun, ISOIS, Instrument` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/ISOIS`
- `PSP ISOIS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/ISOIS/EPI-Hi/HET`
- `PSP ISOIS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/ISOIS/EPI-Hi/LET1`
- `PSP ISOIS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/ISOIS/EPI-Hi/LET2`
- `PSP ISOIS` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/ISOIS/EPI-Lo`
- `PSP SWEAP` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP`
- `PSP SWEAP` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP/SPAN-A`
- `PSP SWEAP` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP/SPAN-B`
- `PSP SWEAP` — `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP/SPC`

**MAVEN — 10 rows**

- `MAVEN Spacecraft Ephemeris Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/Ephemeris`
- `MAVEN Imaging Ultraviolet Spectrograph, IUVS, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/IUVS`
- `MAVEN Langmuir Probe and Waves, LPW, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/LPW`
- `MAVEN Langmuir Probe and Waves, LPW, Extreme Ultraviolet Monitor, EUV, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/LPW/EUV`
- `MAVEN Magnetometer, MAG, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/MAG`
- `MAVEN Neutral Gas and Ion Mass Spectrometer, NGIMS, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/NGIMS`
- `MAVEN Solar Energetic Particle, SEP, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/SEP`
- `MAVEN SupraThermal And Thermal Ion Composition, STATIC, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/STATIC`
- `MAVEN Solar Wind Electron Analyzer, SWEA, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/SWEA`
- `MAVEN Solar Wind Ion Analyzer, SWIA, Instrument` — `https://spase-metadata.org/SMWG/Instrument/MAVEN/SWIA`

**Wind — 6 rows**

- `Wind Hot Plasma and Charged Particles` — `https://spase-metadata.org/SMWG/Instrument/Wind/3DP`
- `Energetic Particle Acceleration, Composition and Transport` — `https://spase-metadata.org/SMWG/Instrument/Wind/EPACT`
- `Wind Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Wind/Ephemeris`
- `Wind Magnetic Field Investigation` — `https://spase-metadata.org/SMWG/Instrument/Wind/MFI`
- `Wind Solar Wind Experiment` — `https://spase-metadata.org/SMWG/Instrument/Wind/SWE`
- `Plasma and Radio Waves` — `https://spase-metadata.org/SMWG/Instrument/Wind/WAVES`

**ACE — 7 rows**

- `Cosmic Ray Isotope Spectrometer` — `https://spase-metadata.org/SMWG/Instrument/ACE/CRIS`
- `ACE Electron Proton Alpha Monitor` — `https://spase-metadata.org/SMWG/Instrument/ACE/EPAM`
- `ACE Magnetic Field Instrument` — `https://spase-metadata.org/SMWG/Instrument/ACE/MAG`
- `Solar Energetic Particle Ionic Charge Analyzer` — `https://spase-metadata.org/SMWG/Instrument/ACE/SEPICA`
- `Solar Isotope Spectrometer` — `https://spase-metadata.org/SMWG/Instrument/ACE/SIS`
- `ACE Solar Wind Electron, Proton and Alpha Monitor` — `https://spase-metadata.org/SMWG/Instrument/ACE/SWEPAM`
- `Ultra-Low Energy Isotope Spectrometer` — `https://spase-metadata.org/SMWG/Instrument/ACE/ULEIS`

**FAST — 5 rows**

- `Electric Field and Langmuir Probe Experiment` — `https://spase-metadata.org/SMWG/Instrument/FAST/EFLP`
- `Electro-Static Analyzers` — `https://spase-metadata.org/SMWG/Instrument/FAST/ESA`
- `FAST Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/FAST/Ephemeris`
- `Tri-Axial Fluxgate and Search-coil Magnetometers on FAST` — `https://spase-metadata.org/SMWG/Instrument/FAST/MAG`
- `Time of Flight Energy Angle Mass Spectrograph` — `https://spase-metadata.org/SMWG/Instrument/FAST/TEAMS`

**Geotail — 3 rows**

- `Geotail Spacecraft Position` — `https://spase-metadata.org/SMWG/Instrument/Geotail/Ephemeris`
- `Geotail Low Energy Particle Experiment` — `https://spase-metadata.org/SMWG/Instrument/Geotail/LEP`
- `MGF on GEOTAIL` — `https://spase-metadata.org/SMWG/Instrument/Geotail/MGF`

**ICON — 4 rows**

- `The Extreme Ultraviolet Spectrograph` — `https://spase-metadata.org/SMWG/Instrument/ICON/EUV`
- `The Far Ultra Violet Imaging Spectrograph` — `https://spase-metadata.org/SMWG/Instrument/ICON/FUV`
- `The Ion Velocity Meter` — `https://spase-metadata.org/SMWG/Instrument/ICON/IVM`
- `Michelson Interferometer for Global High-resolution Thermospheric Imaging` — `https://spase-metadata.org/SMWG/Instrument/ICON/MIGHTI`

**DSCOVR — 3 rows**

- `DSCOVR Instrument for Spacecraft Ephemeris, Orbit and Attitude` — `https://spase-metadata.org/SMWG/Instrument/DSCOVR/Ephemeris`
- `DSCOVR PlasMag Faraday Cup` — `https://spase-metadata.org/SMWG/Instrument/DSCOVR/PlasMag/FaradayCup`
- `DSCOVR PlasMag Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/DSCOVR/PlasMag/FluxgateMagnetometer`

**STEREO — 14 rows**

- `STEREO-A Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/Ephemeris`
- `STEREO-A In situ Measurements of Particles and CME Transients` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/IMPACT`
- `STEREO-A IMPACT Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/IMPACT/MAG`
- `STEREO-A IMPACT Suprathermal Electron Telescope` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/IMPACT/STE`
- `STEREO-A IMPACT Solar Wind Plasma Electron Analyzer` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/IMPACT/SWEA`
- `Plasma and Supra-Thermal Ion Composition` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/PLASTIC`
- `STEREO-A Waves` — `https://spase-metadata.org/SMWG/Instrument/STEREO-A/SWAVES`
- `STEREO-B Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/Ephemeris`
- `STEREO-B In situ Measurements of Particles and CME Transients` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/IMPACT`
- `STEREO-B IMPACT Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/IMPACT/MAG`
- `STEREO-B IMPACT Suprathermal Electron Telescope` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/IMPACT/STE`
- `STEREO-B IMPACT Solar Wind Plasma Electron Analyzer` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/IMPACT/SWEA`
- `Plasma and Supra-Thermal Ion Composition` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/PLASTIC`
- `STEREO-B Waves` — `https://spase-metadata.org/SMWG/Instrument/STEREO-B/SWAVES`

**MarsExpress — 3 rows**

- `Mars Express ASPERA-3` — `https://spase-metadata.org/SMWG/Instrument/MarsExpress/ASPERA3`
- `Mars Express ASPERA-3 Electron Spectrometer` — `https://spase-metadata.org/SMWG/Instrument/MarsExpress/ASPERA3/ELS`
- `Mars Express ASPERA-3 Ion Mass Analyzer` — `https://spase-metadata.org/SMWG/Instrument/MarsExpress/ASPERA3/IMA`

**VenusExpress — 3 rows**

- `Venus Express ASPERA-4` — `https://spase-metadata.org/SMWG/Instrument/VenusExpress/ASPERA4`
- `Venus Express ASPERA-4 Electron Spectrometer` — `https://spase-metadata.org/SMWG/Instrument/VenusExpress/ASPERA4/ELS`
- `Venus Express ASPERA-4 Ion Mass Analyzer` — `https://spase-metadata.org/SMWG/Instrument/VenusExpress/ASPERA4/IMA`

**Akebono — 3 rows**

- `Akebono Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Akebono/Ephemeris`
- `Plasma Wave Observation and Sounder Experiments` — `https://spase-metadata.org/SMWG/Instrument/Akebono/PWS`
- `AKEBONO Radiation Dose, RDM, Instrument` — `https://spase-metadata.org/SMWG/Instrument/Akebono/RDM`

**ELFIN — 4 rows**

- `Electron Losses and Fields Investigation, ELFIN` — `https://spase-metadata.org/SMWG/Instrument/ELFIN/A/Ephemeris`
- `Electron Losses and Fields Investigation, ELFIN` — `https://spase-metadata.org/SMWG/Instrument/ELFIN/B/Ephemeris`
- `The Electron Losses and Fields Investigation` — `https://spase-metadata.org/NASA/Instrument/ELFIN/A/EPD`
- `The Electron Losses and Fields Investigation` — `https://spase-metadata.org/NASA/Instrument/ELFIN/B/EPD`

The two EPD rows share one display name, so the identifier is what distinguishes ELFIN-A from
ELFIN-B — the same convention used for the per-probe MMS, RBSP, THEMIS and Cluster expansions above,
where several rows also share a name. They resolve through the single-agency-row branch of the
resolution rule: unlike ELFIN's Ephemeris rows, which exist in both `SMWG/Instrument/ELFIN/{A,B}/
Ephemeris` and `NASA/Instrument/ELFIN/{A,B}/Ephemeris` form and are therefore recorded at their SMWG
identifiers, **EPD has no `SMWG` counterpart at all** — `NASA/Instrument/ELFIN/A/EPD` and
`.../B/EPD` are the only EPD rows in the vocabulary, both `type = 1`, both SPASE-backed, both named
`The Electron Losses and Fields Investigation` with abbreviation `ELFIN`. With no duplicate to break a
tie against, the single non-SMWG match is the correct value. Their SPASE definition confirms the
match: "ELFIN will be flying two energetic particle detectors (EPDs). It has one EPD for ions (EPDI)
and one for electrons (EPDE)" — exactly the `pif`/`pef`/`pis`/`pes` products `elf_load_epd.pro`
loads. Per-probe expansion is licensed by that routine's own declaration that "valid values for elf
probes are ['a','b']". ELFIN's missing-row gap is therefore narrower than it first looks: it covers
FGM and MRMa/MRMi, as the omission entry below records, and not EPD — `ELFIN/{A,B}/Ephemeris` are not
the only ELFIN rows in the vocabulary.

**Cassini — 3 rows**

- `Cassini Orbiter Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/Cassini/Ephemeris`
- `Dual Technique Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/Cassini/MAG`
- `Cassini Radio And Plasma Wave Science` — `https://spase-metadata.org/SMWG/Instrument/Cassini/RPWS`

**GOES — 34 rows**

- `GOES Triaxial Fluxgate Magnetometer on GOES  8` — `https://spase-metadata.org/SMWG/Instrument/GOES/8/MAG`
- `GOES 8 Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/GOES/8/Ephemeris`
- `GOES Triaxial Fluxgate Magnetometer on GOES 9` — `https://spase-metadata.org/SMWG/Instrument/GOES/9/MAG`
- `GOES 9 Ephemeris` — `https://spase-metadata.org/SMWG/Instrument/GOES/9/Ephemeris`
- `GOES Triaxial Fluxgate Magnetometer on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/10/MAG`
- `GOES 10 Position` — `https://spase-metadata.org/SMWG/Instrument/GOES/10/Ephemeris`
- `GOES Triaxial Fluxgate Magnetometer on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/11/MAG`
- `GOES 11 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/11/Ephemeris`
- `GOES Triaxial Fluxgate Magnetometer on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/12/MAG`
- `GOES 12 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/12/Ephemeris`
- `Triaxial Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/GOES/13/MAG`
- `GOES 13 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/13/Ephemeris`
- `Triaxial Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/GOES/14/MAG`
- `GOES 14 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/14/Ephemeris`
- `Triaxial Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/GOES/15/MAG`
- `GOES 15 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/15/Ephemeris`
- `Space Environment Monitor` — `https://spase-metadata.org/SMWG/Instrument/GOES/8/SEM`
- `Space Environment Monitor on GOES  9` — `https://spase-metadata.org/SMWG/Instrument/GOES/9/SEM`
- `Space Environment Monitor` — `https://spase-metadata.org/SMWG/Instrument/GOES/10/SEM`
- `Environment Monitor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/11/SEM`
- `Space Environment Monitor` — `https://spase-metadata.org/SMWG/Instrument/GOES/12/SEM`
- `Space Environment Monitor` — `https://spase-metadata.org/SMWG/Instrument/GOES/13/SEM`
- `Space Environment Monitor` — `https://spase-metadata.org/SMWG/Instrument/GOES/14/SEM`
- `Space Environment Monitor` — `https://spase-metadata.org/SMWG/Instrument/GOES/15/SEM`
- `Energetic Particle Sensor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/13/EPS`
- `Solar X-ray Sensor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/13/XRS`
- `Energetic Particle Sensor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/14/EPS`
- `Solar X-ray Sensor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/14/XRS`
- `Energetic Particle Sensor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/15/EPS`
- `Solar X-ray Sensor on GOES` — `https://spase-metadata.org/SMWG/Instrument/GOES/15/XRS`
- `Triaxial Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/GOES/16/MAG`
- `GOES 16 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/16/Ephemeris`
- `Triaxial Fluxgate Magnetometer` — `https://spase-metadata.org/SMWG/Instrument/GOES/17/MAG`
- `GOES 17 Positions` — `https://spase-metadata.org/SMWG/Instrument/GOES/17/Ephemeris`

**NOAA — 2 rows**

- `Space Environment Monitor-2` — `https://spase-metadata.org/SMWG/Instrument/NOAA/18/SEM-2`
- `Space Environment Monitor-2` — `https://spase-metadata.org/SMWG/Instrument/NOAA/19/SEM-2`

**SOHO — 3 rows**

- `Charge, Element, and Isotope Analysis System` — `https://spase-metadata.org/SMWG/Instrument/SOHO/CELIAS`
- `Comprehensive Suprathermal and Energetic Particle Instrument` — `https://spase-metadata.org/SMWG/Instrument/SOHO/COSTEP`
- `Energetic and Relativistic Nuclei and Electrons` — `https://spase-metadata.org/SMWG/Instrument/SOHO/ERNE`

**IMP8 — 2 rows**

- `IMP 8 Magnetic Field Experiment` — `https://spase-metadata.org/SMWG/Instrument/IMP8/MAG`
- `IMP 8 Solar Plasma Faraday Cup` — `https://spase-metadata.org/SMWG/Instrument/IMP8/PLS`

**OMNI — 1 row**

- `OMNI Instrument` — `https://spase-metadata.org/SMWG/Instrument/OMNI`

**SECS — 1 row**

- `Spherical Elementary Current Systems Instrument` — `https://spase-metadata.org/SMWG/Instrument/SECS/Magnetometer`

**Why this row applies even though SPEDAS reads only the derived current product.** The question the
plug-in raises is whether SPEDAS consumes raw magnetometer readings or only the already-inverted SECS
currents, and the code answers it unambiguously: **only the derived product.**
`projects/secs/secs_load_data.pro` accepts exactly two datatypes, `['eics', 'seca']`, and fetches
10-second files `EICSYYYYMMDD_hhmmss.dat` / `SECSYYYYMMDD_hhmmss.dat` from
`http://vmo.igpp.ucla.edu/data1/SECS`. `eic_read_ascii_data.pro` reads four columns — `lat`, `long`,
`jx`, `jy`, the equivalent ionospheric current vectors — and `sec_read_ascii_data.pro` reads three —
`lat`, `long`, `amp`, the spherical elementary current amplitudes. No magnetic field component is read
anywhere in the plug-in.

That nevertheless resolves *to this row*, because the row is not a physical magnetometer. Its SPASE
definition reads: "The Spherical Elementary Current Systems instrument is a virtual instrument
representing the collection of ground magnetometer arrays used to derive spherical elementary currents
over North America and Greenland at 10 s resolution… the SECS instrument is used as a proxy for the set
of possible contributing ground magnetometers." So the virtual instrument's product *is* the 10-second
current files SPEDAS reads — the cadence in the definition matches the loader exactly — and SPEDAS also
consumes the proxy's membership directly: `secs_read_stations.pro` reads the day's
`Stat<YYYYMMDD>.dat` roster of contributing stations ("the name of the stations used to derive the SECS
eics and seca data"), `secs_stations2tplot.pro` turns it into the `secs_stations` tplot variable, and
`eics_overlay_plots.pro` / `seca_overlay_plots.pro` plot those stations on the mosaic maps. Reading the
day-varying station membership is precisely what the definition describes as the instrument's content.

Resolution is unambiguous. Exactly one `type = 1` SMWG row matches: `SMWG/Instrument/SECS/Magnetometer`.
The only other candidate, `NSF/Instrument/Ground/SouthernSECS/Magnetometer` ("Southern Hemisphere
Spherical Elementary Current Systems Instrument"), is a **different entity** — SPEDAS's plug-in covers
the North American and Greenland array, as its plot bounds confirm (`eics_overlay_plots.pro` sets
`yrange = [30,80]`, `xrange = [220,330]`, i.e. 30–80°N, 140–30°W), and `southern` occurs nowhere in
`projects/secs/`. The corresponding observatory row is recorded in Field 32; recording both levels is
correct here because SPASE models the same virtual entity at both.

**Polar — 1 row**

- `Polar Plasma Waves Investigation` — `https://spase-metadata.org/SMWG/Instrument/POLAR/PWI`

`general/key_param/load_po_pwi.pro` is a dedicated Polar Plasma Wave Instrument loader — "Loads Polar
Plasma Wave Instrument key parameter data into 'tplot' variables" — reading the SFR-A/SFR-B average and
peak electric and magnetic spectra (`SFRA_Av_E`, `SFRB_Pk_M` and the rest) plus `Fce`, `Fcp`, `FcO`,
`MLAT`, `L_Shell` support variables, and storing eight spectrogram tplot variables. It is the same kind
of routine, from the same 1999-vintage ISTP key-parameter family, as the SOHO and IMP-8 loaders recorded
above, and carries the same legacy caveat: it expects a locally staged master index file
(`masterfile = 'po_k0_pwi_files'`) rather than a configured remote source.

Resolution is unambiguous: exactly one `type = 1` row sits at `SMWG/Instrument/POLAR/PWI`, and the
CDPP-AMDA Polar instrument mirrors cover Ephemeris, HYDRA, MFE and Models but not PWI, so there is no
tie to break. **Polar is recorded at both instrument and observatory level**, on the same footing as
the SOHO and IMP-8 entries: dedicated per-instrument support that is genuinely shipped in 6.1,
carrying the legacy caveat rather than being disqualified by it. Omitting Polar while recording SOHO
and IMP-8 would be the inconsistency, not including it.

**The claim that "the vocabulary has no Polar observatory row and no Polar instrument row" is false,
and it must not be reused to drop these entries.** The vocabulary carries 20 rows on Polar paths: 14
`SMWG/Instrument/POLAR/*` instrument rows, the `SMWG/Observatory/POLAR` row recorded in Field 32,
four `CNES/Instrument/CDPP-AMDA/POLAR/*` mirrors and the `CNES/Observatory/CDPP-AMDA/POLAR` mirror.

Only PWI is recorded, not the other 13 Polar instrument rows (CAMMICE and its HIT/MICS sensors, CEPPAD,
EFI, HYDRA, MFE, PIXIE, TIDE, TIMAS, UVI, VIS, Ephemeris), and the bound is a fact about the tree
rather than a choice of granularity: `load_po_pwi.pro` is the only `load_po_*` routine in
`general/key_param/`, so nothing in the tree supports the rest.

**No entry in this field is ambiguous.** Every one of the 275 entries above resolves to exactly one
SPASE row under the rule stated at the top of this field. The two instrument/observatory ambiguities
this record once carried, CARISMA and BAS, are resolved in Field 32.

**Instruments considered and deliberately not recorded, with reasons.** These are the searches a
future agent should not repeat.

- **GOES SUVI — excluded on positive evidence, not oversight.** The vocabulary has four Solar
  Ultraviolet Imager rows (`NOAA/Instrument/GOES/{16,17,18,19}/SUVI`) and it would be easy to attach
  them to a GOES-supporting package. `projects/goesr/goesr_load_data.pro` lists its complete valid
  datatype set as `'mag'`, `'xrs'`, `'mpsh'` and `'sgps'`; SUVI is absent, and there is no SUVI
  loader anywhere in the tree. SPEDAS does not support SUVI.
- **GOES-16/17 EXIS and SEISS have no SPASE instrument rows.** SPEDAS supports their products
  (`'xrs'` → EXIS X-Ray Sensor, `'mpsh'` → SEISS MPS-HI, `'sgps'` → SEISS SGPS), but the vocabulary
  has only three `type = 1` rows per GOES-16/17 spacecraft: `SMWG/Instrument/GOES/1{6,7}/MAG`,
  `SMWG/Instrument/GOES/1{6,7}/Ephemeris` and `NOAA/Instrument/GOES/1{6,7}/SUVI` — no EXIS or SEISS
  row at any path. (SUVI exists but is excluded on its own evidence, immediately above; it is easy to
  overlook, leaving MAG and Ephemeris looking like the only GOES-16/17 instrument rows.) Applying the
  instrument→observatory fallback, the EXIS and SEISS association is carried at observatory level by `SMWG/Observatory/GOES/16` and `/17` in Field 32.
- **GOES 8–12 XRS has no row either.** `GOES/8/SXM` (Solar X-ray Monitor) and `GOES/12/SXI` (Solar
  X-Ray Imager) exist but are different instruments from the XRS that `goes_load_data` reads, so
  using them would be a mis-association; the observatory rows carry it instead.
- **MMS FSM** (the merged FGM–SCM product, `mms_load_fsm.pro`) has no SPASE row of its own; the
  constituent `FIELDS/FGM` and `FIELDS/SCM` rows are recorded for all four probes.
- **THEMIS FFT and FIT** (`thm_load_fft`/`thm_cal_fft`, `thm_load_fit`/`thm_cal_fit`) have no SPASE
  rows. FFT is a Digital Fields Board mode, partly covered by the recorded `FBK` (Filter Bank) rows;
  FIT is an on-board spin-fit product, adjacent to the recorded `MOM` rows.
- **ERG/Arase instruments — zero rows exist.** The tree has a full per-instrument plug-in tree
  (`projects/erg/satellite/erg/{mgf,pwe,hep,xep,lepe,lepi,mep,orb}/`) and the observatory is already
  associated in HSSI, but a search of the vocabulary for any `type = 1` row under an `ARASE` or `ERG`
  path returns nothing. The association is carried at observatory level only. Measured by supported
  instruments left unrepresentable, this is the largest of the *missing-row* gaps in this field —
  eight instrument subtrees against zero rows, where ELFIN loses two and Venus Express one — and it is
  an upstream vocabulary gap, not an extraction failure. (The larger *bounded* exclusions below,
  BARREL and the ground-station families, are a different case: there the rows exist and the choice is
  granularity.)
- **ELFIN FGM and MRMa/MRMi — no rows; EPD and Ephemeris are recorded above.** The vocabulary carries
  six `type = 1` ELFIN rows (eight on ELFIN paths in total, the other two being the A and B observatory
  rows), and every one of the six is Ephemeris or EPD: `SMWG/Instrument/ELFIN/{A,B}/Ephemeris`, their
  `NASA/Instrument/ELFIN/{A,B}/Ephemeris` mirrors, and `NASA/Instrument/ELFIN/{A,B}/EPD`. There is no
  row of any kind for the fluxgate magnetometer or the two magnetoresistive magnetometers, despite
  dedicated support for all three: `projects/elfin/load_data/elf_load_fgm.pro`, `elf_load_mrma.pro`
  and `elf_load_mrmi.pro`, with the calibrators `projects/elfin/cal_data/{elf_cal_fgm,elf_cal_mrma,
  elf_cal_mrmi}.pro`, the FGM spin-fit transforms `elf_fgm_fsp_gei2{ndw,obw}.pro`, the segment loaders
  `projects/elfin/plots/elf_load_fgm_{fast,survey}_segments.pro` and the three test suites
  `projects/elfin/tests/elf_{fgm,mrma,mrmi}_load_cltestsuite.pro`. That is an upstream vocabulary gap,
  not missing support; observatory-level association already exists for both CubeSats.
- **Venus Express MAG** — `projects/vex/mag/vex_mag_load.pro` is dedicated support, but the
  vocabulary's only Venus Express instrument rows are the five ASPERA-4 rows. Carried by the
  `SMWG/Observatory/VenusExpress` row already stored.
- **MEX/VEX ASPERA NPD and NPI** — rows exist, but SPEDAS loads only ELS and IMA (plus the derived
  solar-wind monitor `mex_asp_swm_load.pro`/`vex_asp_swm_load.pro`). Not supported, not recorded.
- **RBSP RPS** (Relativistic Proton Spectrometer) — a row exists for both probes, but there is no RPS
  loader in `general/missions/rbsp/`.
- **Wind SMS (and MASS/STICS/SWICS) and TGRS** — rows exist, but `general/key_param/` has no
  corresponding `load_wi_*` routine.
- **ACE SWICS and SWIMS** — rows exist; there is no `load_ace_swics` or `load_ace_swims`.
- **Geotail CPI, EFD, EPIC and PWI** — rows exist; `geotail_load_data.pro`'s datatype list is exactly
  `'lep', 'mgf', 'orbit'`.
- **Akebono LEP, SMS, TED and ATV** — rows exist; `projects/akebono/` has only `pws`, `rdm` and `orb`.
- **Juno FGM, JADE, JEDI and Waves** — SPEDAS reaches Juno data through a generic das2 dataset query
  (`projects/juno/juno_load_data.pro` builds
  `'server?server=dataset&dataset='+datatype+...` and hands the result to `das2tplot.pro`), so no
  specific instrument is named in non-example code; Juno Waves appears only as a das2dlm example crib
  (`external/das2dlm/examples/das2dlm_crib_basic_juno.pro`), and example name-drops are explicitly
  excluded by the relevance gate. The only SMWG Juno instrument row is `Juno/Ephemeris`; `FGM`,
  `JADE`, `JEDI` and `WAVES` exist solely as `CNES/Instrument/CDPP-AMDA/Juno/*` mirrors. Association
  carried at observatory level by the new `SMWG/Observatory/Juno` entry.
- **Galileo** — `external/das2dlm/examples/das2dlm_crib_basic_galileo.pro` is an example crib only,
  with no loader in `projects/`. Excluded as a demo mention.
- **MetOp SEM-2 — a genuine ambiguity, recorded as a documented omission, and the reasoning
  matters.** `poes_load_data.pro` names `metop2` among its example probes, and the
  generic `/noaa/<probe>/sem2_fluxes-2sec/` path would serve it. The vocabulary has
  `SMWG/Instrument/MetOp/A/SEM-2` and `SMWG/Instrument/MetOp/B/SEM-2`, and — decisively — the two
  *observatory* rows `SMWG/Observatory/MetOp/A` and `SMWG/Observatory/MetOp/B` **both carry the
  name `MetOp-A`**, an upstream defect. So neither the instrument choice nor the observatory fallback
  can be made safely: `metop2` is the launch designation of MetOp-A, but a row named `MetOp-A` at the
  `/MetOp/B` path makes any pick unverifiable. Compounding it, the probe list is introduced with
  "i.e." (an example) rather than "valid values are", so the code does not actually assert MetOp
  support the way it asserts NOAA-18/19. Omitted with this note; a future refresh can record it if
  upstream fixes the duplicate observatory name.
- **NOAA-15, -16 and -17 SEM-2** — rows exist and the path template would serve them, but
  `poes_load_data.pro` names only `noaa18`, `noaa19` and `metop2`. Inferring the rest would be a
  guess rather than the concrete evidence the multi-row expansion rule requires.
- **Cluster WBD — omitted as an unresolvable same-entity collision.** `projects/cluster/wbd/` is
  dedicated support, but the vocabulary carries eight rows all named `Wide Band Data`:
  `SMWG/Instrument/Cluster-{Rumba,Salsa,Samba,Tango}/WBD` and
  `SMWG/Instrument/Cluster/C{1,2,3,4}/WBD`. Those are two parallel SPASE naming schemes for the same
  four physical instruments (Rumba = C1, Salsa = C2, Samba = C3, Tango = C4), both under `SMWG`, so
  the SMWG tie-breaker cannot separate them and nothing in the tree selects a scheme. The other
  eleven Cluster instruments have no such duplicate and are recorded. Cluster is already associated
  at observatory level.
- **The other thirteen Polar instruments** — CAMMICE (and its HIT and MICS sensors), CEPPAD, EFI,
  HYDRA, MFE, PIXIE, TIDE, TIMAS, UVI, VIS and Ephemeris all have `SMWG/Instrument/POLAR/*` rows, but
  `general/key_param/` contains only `load_po_pwi.pro`, so only PWI is supported and only PWI is
  recorded above. Polar itself is recorded at both levels, instrument and observatory.
- **BARREL per-payload instruments — a bounded exclusion, stated so it can be revisited.** The
  vocabulary carries 330 BARREL instrument rows, which decompose exactly as 54 balloon payloads
  (`1A`, `1B`, `1C`, …) × six instruments (`XRI`, `MAG`, `Ephemeris`, `DataProcessingUnit`,
  `EngineeringDataInterface`, `OpticalPhotometer`) = 324, plus six mission-level rows carrying the same
  six instrument names with no payload segment (`SMWG/Instrument/BARREL/XRI` and its siblings). There
  are 54 matching `type = 2` payload observatory rows. `projects/barrel/barrel_load_*.pro` takes a payload identifier and supports
  the array generically; the tree does not enumerate a supported-payload list, so a 330-row expansion
  would rest on inference rather than evidence, and would by itself outweigh every other mission in
  this field. BARREL is already associated at observatory level. Named here with the exact row family
  so a future refresh can expand it if HSSI wants per-payload granularity.
- **Ground-network station-level rows — the same bounded exclusion.** SPEDAS loads THEMIS GBO/EPO
  magnetometers and all-sky imagers, CARISMA, Greenland, BAS, MACCS, GIMA, IUGONET/NIPR, MAGDAS, the
  210° magnetic meridian chain, CPMN, EISCAT and SuperDARN. Three of those families are large enough
  to be worth sizing, counted the same way in each case — **`type = 2` rows whose identifier begins
  with the literal path prefix given**: `IUGONET/Observatory/ICSWSE/MAGDAS/` → **62**;
  `IUGONET/Observatory/ISEE/MM210/` → **30**; `IUGONET/Observatory/ICSWSE/CPMN/` → **54**. Each has an
  equal number of `type = 1` station-instrument rows, so the totals under either type are 124, 60 and
  108. Two counting traps to note: a substring search for "MAGDAS" returns 65 observatory rows rather
  than 62, the extra three being FM-CW radar stations under the sibling prefix
  `IUGONET/Observatory/ICSWSE/MAGDAS-FMCW/{MNL,PTK,SAS}` rather than magnetometer stations; and a
  substring search for "CPMN" returns 108, which is the combined instrument-plus-observatory total,
  not the 54 observatories.

  The vocabulary models most of these networks only at station level, which across all of them would
  be many hundreds of rows. Field 32 instead records *network-level* rows wherever the vocabulary
  offers one: the four THEMIS ground rows, `SuperDARN`, `Ground/CARISMA` and `Ground/BAS`. That is
  proportionate granularity for a framework record, and the station families are named here so the
  choice is reversible.

  Two of those networks show why network level is the right level, in opposite ways. **CARISMA has
  station rows, but they cover only part of what SPEDAS supports**: the vocabulary carries 12
  station-instrument rows named `CARISMA Magnetometer at <site>` (at
  `SMWG/Instrument/{Contwoyto,Dawson,EskimoPoint,FortMcMurray,FortSimpson,FortSmith,Gillam,IslandLake,
  Pinawa,RabbitLake,RankinInlet,Taloyoak}/Magnetometer`) with 12 matching station-observatory rows
  named by four-letter site code. Those 12 reconcile exactly against the loader as 7 of the 23 sites
  `thm_load_carisma_gmag.pro` fetches directly (CONT, DAWS, ESKI, ISLL, MCMU, RABB, TALO) plus the 5
  its header says are mirrored by THEMIS and loaded through `thm_load_gmag` instead (FSIM, FSMI, GILL,
  PINA, RANK) — leaving 16 supported sites with no row at all. A station-level expansion would
  therefore be both large and incomplete. **BAS has no station rows whatsoever**: the vocabulary
  carries exactly two BAS rows, the network-level `Observatory/BAS` and `Observatory/Ground/BAS` pair,
  and nothing beneath a `BAS/` subpath, so network level is the only representation available.
- **Solar Orbiter — recorded as a negative result because two things invite the error.** The HSSI
  keyword list contains both `solar orbiter` and `solo` (inherited from Zenodo), and the tree contains
  `projects/SPP/fields/l1/l1_ephem/spp_fld_ephem_solo_{hg,rtn,vso}_load_l1.pro`. Those routines load
  **Solar Orbiter position vectors out of PSP FIELDS L1 ephemeris files** — PSP ancillary data about
  where another spacecraft was, not Solar Orbiter instrument support. Searching the whole tree for
  `solar orbiter` and `solo_` outside `projects/SPP/` yields one hit, `general/spice/orrery.pro`, a
  solar-system orrery plot. SPEDAS 6.1 supports no Solar Orbiter instrument or dataset. Neither
  `ESA/Observatory/SolarOrbiter` nor any Solar Orbiter instrument row is recorded.
- **IMAGE mission** — the keyword `image` is stored (from Zenodo's `IMAGE`) and
  `SMWG/Observatory/IMAGE` ("Imager for Magnetopause-to-Aurora Global Exploration") exists, but there
  is no IMAGE loader in the tree. `load_image`, `im_load`, `si12` and `si13` return no hits at all.
  `wic` needs care rather than a bare count: it matches 99 files, but every occurrence is inside an
  unrelated token — overwhelmingly the STEREO PLASTIC composition variables `swica`/`swics` and their
  derivatives, plus `twice`, `Greenwich` and `which` — and never as a reference to IMAGE's Wideband
  Imaging Camera. Not recorded at either level.
- **Lomonosov, LuSEE, SWFO, ESCAPADE, IUGONET as an entity** — `projects/lomonosov/`,
  `projects/lusee/`, `projects/SWFO/` and `projects/escapade/` are all real plug-ins, but searching the
  vocabulary for `Lomonosov`, `LuSEE`, `SWFO`, `ESCAPADE` and `STIS` in either the identifier or the
  name returns zero rows of either type, so there is nothing to resolve to at any level. IUGONET is
  handled only through its member stations. SECS does **not** belong in this group:
  `SMWG/Instrument/SECS/Magnetometer` exists and is recorded above.
- **Agency-mirror rows generally** — `CNES/Instrument/CDPP-AMDA/*`, `CNES/Instrument/CDPP-Archive/*`
  and `NASA/Instrument/*` duplicates of recorded SMWG instruments (Wind MFI, Wind WAVES, Wind
  Ephemeris, ACE EPAM, Geotail MGF, STEREO-A/B PLASTIC and Ephemeris, VEX ASPERA-4 IMA, ELFIN A/B
  Ephemeris, Cassini MAG, SOHO COSTEP and ERNE, and the THEMIS/ARTEMIS CDPP-AMDA set) are
  deliberately not recorded alongside their SMWG counterparts. They describe the same physical
  instruments in a different catalogue; recording both would double-count each instrument.

### 32. Related Observatories (OPTIONAL)

54 observatory associations: 27 of the 28 already stored, plus 27 additions. One stored value,
`KOMPSAT`, was removed as a mis-resolution; the reasoning is below.

Stored and retained (27), with their resolved SPASE identifiers:

- `Acceleration, Reconnection, Turbulence, Electrodynamics of the Moon’s Interaction with the Sun` — `https://spase-metadata.org/SMWG/Observatory/ARTEMIS`
- `Advanced Composition Explorer` — `https://spase-metadata.org/SMWG/Observatory/ACE`
- `AKEBONO` — `https://spase-metadata.org/SMWG/Observatory/Akebono`
- `Balloon Array for Radiation-belt Relativistic Electron Losses` — `https://spase-metadata.org/SMWG/Observatory/BARREL`
- `Cluster` — `https://spase-metadata.org/SMWG/Observatory/Cluster`
- `Deep Space Climate Observatory, DSCOVR` — `https://spase-metadata.org/SMWG/Observatory/DSCOVR`
- `Electron Losses and Fields Investigation A, CubeSat` — `https://spase-metadata.org/SMWG/Observatory/ELFIN/A`
- `Electron Losses and Fields Investigation B, CubeSat` — `https://spase-metadata.org/SMWG/Observatory/ELFIN/B`
- `Emirates Mars Mission` — `https://spase-metadata.org/SMWG/Observatory/EMM`
- `Exploration of energization and Radiation in Geospace` — `https://spase-metadata.org/SMWG/Observatory/ARASE`
- `Fast Auroral Snapshot` — `https://spase-metadata.org/SMWG/Observatory/FAST`
- `Geomagnetic Tail Lab` — `https://spase-metadata.org/SMWG/Observatory/Geotail`
- `Geostationary Operational Environmental Satellites` — `https://spase-metadata.org/SMWG/Observatory/GOES`
- `Heliophysics Environmental and Radiation Measurement Experiment Suite` — `https://spase-metadata.org/SMWG/Observatory/HERMES`
- `Ionospheric Connection` — `https://spase-metadata.org/SMWG/Observatory/ICON`
- `ISTP/Wind` — `https://spase-metadata.org/SMWG/Observatory/Wind`
- `Kaguya` — `https://spase-metadata.org/SMWG/Observatory/KAGUYA`
- `Magnetosphere-Ionosphere Coupling in the Alfvén resonator` — `https://spase-metadata.org/SMWG/Observatory/MICA`
- `Magnetospheric Multiscale` — `https://spase-metadata.org/SMWG/Observatory/MMS`
- `Mars Atmosphere and Volatile EvolutioN` — `https://spase-metadata.org/SMWG/Observatory/MAVEN`
- `Mars Express` — `https://spase-metadata.org/SMWG/Observatory/MarsExpress`
- `Parker Solar Probe` — `https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe`
- `Polar-orbiting Operational Environmental Satellite` — `https://spase-metadata.org/SMWG/Observatory/POES`
- `Solar-Terrestrial Relations Observatory` — `https://spase-metadata.org/SMWG/Observatory/STEREO`
- `Time History of Events and Macroscale Interactions during Substorms` — `https://spase-metadata.org/SMWG/Observatory/THEMIS`
- `Van Allen Probes` — `https://spase-metadata.org/SMWG/Observatory/RBSP`
- `Venus Express` — `https://spase-metadata.org/SMWG/Observatory/VenusExpress`

All 27 resolve to live SPASE-backed rows; none is an identifierless legacy row. Every one is
independently justified by a `projects/` or `general/missions/` plug-in, so none was removed on
relevance grounds — the single removal, `KOMPSAT`, was a wrong-entity mis-resolution rather than an
irrelevant mission. Two further matters are durable: an identifier-form observation about six of the
retained rows, and the rationale for that one removal.

**Six retained rows once used the `.html` identifier variant while a bare-form row also existed** —
EMM, ARASE, HERMES, KAGUYA, MICA and POES — and all six are recorded above under the bare form.
(KOMPSAT1 was a seventh, but it is removed outright below on wrong-entity grounds, which is a separate
question from identifier form.) The two forms were the same SPASE resource, and the resolution ladder
prefers the bare one, but they were *different HSSI rows with different display names*
(`Emirates Mars Mission` vs `Emirates Mars Mission (EMM)`; `Exploration of energization and
Radiation in Geospace` with abbreviation `ERG` vs the long "now known as Arase" form;
`Polar-orbiting Operational Environmental Satellite` vs the same with `(POES)` appended).

**Normalizing them was once considered and declined; that decision is superseded.** The reasoning then
was that normalization would be a removal-plus-addition changing user-visible display names while
gaining nothing evidentially, since both forms denote one SPASE resource. What that reasoning did not
weigh is that the `.html` form was never a registered identifier: the maintained upstream registry
publishes **no `.html` identifier at all**, for any instrument or observatory, so those rows were
landing-page URL artifacts rather than a second legitimate form of the identifier. HSSI's vocabulary
has since been consolidated onto the upstream identifiers, retiring the `.html` rows, so these six
entries now carry the surviving bare rows with those rows' stored names copied verbatim. The six name
changes are a consequence of that consolidation, not an unevidenced rename.

The durable warning is the reason this is recorded at all: **a future agent resolving these six
missions from scratch will land on the bare-form rows, which is exactly what is recorded above.** The
older display names quoted in this note are history rather than an alternative to re-adopt, and the
`.html` form should not be reintroduced.

**`KOMPSAT` was removed as a wrong-entity mis-resolution.** The stored row was
`SMWG/Observatory/KOMPSAT1.html`, whose bare form is named "Korean Multi-Purpose Satellite" with
abbreviation `KOMPSAT-1` — the 1999 spacecraft. What SPEDAS actually supports is SOSMAG on
**GEO-KOMPSAT-2A**, a different and much later satellite: `projects/sosmag/sosmag_readme.txt` states
"This is a plugin for the magnetometer data of the SOSMAG (Service Oriented Spacecraft Magnetometer)
instrument aboard the GEO-KOMPSAT-2A satellite (geostationary orbit at 128.2 East)" and its example
URLs request `spase://SSA/NumericalData/GEO-KOMPSAT-2A/esa_gk2a_sosmag_recalib`. The stored value
therefore associated SPEDAS with a spacecraft it does not support, so it is gone.

**The durable part is that GEO-KOMPSAT-2A has no row, so this must not be "fixed" by re-adding
KOMPSAT.** Searching the vocabulary for `KOMPSAT`, `GK2A`, `GEO-KOMPSAT` and `SOSMAG` at the time
returned exactly two rows — the `.html`/bare pair for one SPASE resource, `SMWG/Observatory/KOMPSAT1.html`
(display name `KOMPSAT`, the row that was stored) and `SMWG/Observatory/KOMPSAT1` (display name
`Korean Multi-Purpose Satellite`, abbreviation `KOMPSAT-1`) — and only the bare row survives the
vocabulary consolidation. There is no GEO-KOMPSAT-2A row at any
level under any of those four terms. A correct fresh resolution is a documented omission, and it stays
one until an upstream heliophysics.net/SPASE refresh creates a GK2A row — at which point the
association becomes recordable at last. The project's own interest in the mission survives regardless
as the Field 16 keyword `kompsat`, which is the right home for a project-asserted association the
controlled vocabulary cannot express.

Additions (27):

- `OMNI` — `https://spase-metadata.org/SMWG/Observatory/OMNI`
- `Polar` — `https://spase-metadata.org/SMWG/Observatory/POLAR`
- `Spherical Elementary Current Systems` — `https://spase-metadata.org/SMWG/Observatory/SECS`
- `Cassini Orbiter` — `https://spase-metadata.org/SMWG/Observatory/Cassini`
- `Juno Orbiter` — `https://spase-metadata.org/SMWG/Observatory/Juno`
- `Solar and Heliospheric Observatory` — `https://spase-metadata.org/SMWG/Observatory/SOHO`
- `Explorer 50` — `https://spase-metadata.org/SMWG/Observatory/IMP8`
- `ISTP/Equator-S` — `https://spase-metadata.org/SMWG/Observatory/Equator-S`
- `SuperDARN` — `https://spase-metadata.org/SMWG/Observatory/SuperDARN`
- `NASA THEMIS GBO Ground Stations` — `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/UCLA-GBO`
- `NASA THEMIS EPO Ground Stations` — `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/UCLA-EPO`
- `Canadian Magnetometer Array` — `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/CANMAG`
- `NASA THEMIS Ground Stations in Alaska` — `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/GIMA`
- `Advanced TIROS-N` — `https://spase-metadata.org/SMWG/Observatory/NOAA/18`
- `NOAA-N Prime` — `https://spase-metadata.org/SMWG/Observatory/NOAA/19`
- `1994-022A` — `https://spase-metadata.org/SMWG/Observatory/GOES/8`
- `1995-025A` — `https://spase-metadata.org/SMWG/Observatory/GOES/9`
- `1997-019A` — `https://spase-metadata.org/SMWG/Observatory/GOES/10`
- `2000-022A` — `https://spase-metadata.org/SMWG/Observatory/GOES/11`
- `2001-031A` — `https://spase-metadata.org/SMWG/Observatory/GOES/12`
- `Geostationary Operational Environmental Satellite 13` — `https://spase-metadata.org/SMWG/Observatory/GOES/13`
- `Geostationary Operational Environmental Satellite 14` — `https://spase-metadata.org/SMWG/Observatory/GOES/14`
- `Geostationary Operational Environmental Satellite 15` — `https://spase-metadata.org/SMWG/Observatory/GOES/15`
- `Geostationary Operational Environmental Satellite 16` — `https://spase-metadata.org/SMWG/Observatory/GOES/16`
- `Geostationary Operational Environmental Satellite 17` — `https://spase-metadata.org/SMWG/Observatory/GOES/17`
- `Canadian Array for Realtime Investigations of Magnetic Activity` — `https://spase-metadata.org/SMWG/Observatory/Ground/CARISMA`
- `British Antarctic Survey` — `https://spase-metadata.org/SMWG/Observatory/Ground/BAS`

Evidence for each addition:

- **`OMNI`** — `projects/omni/omni_load_data.pro` with its own config, plug-in and GUI import
  routines; the Field 17 value `OMNIWeb` is the source, and this is the mission-level counterpart.
- **`Polar`** — `general/key_param/load_po_pwi.pro`, the dedicated Polar Plasma Wave Instrument
  key-parameter loader detailed in Field 31, where the matching `SMWG/Instrument/POLAR/PWI` row is also
  recorded. Exactly one `type = 2` row sits at `SMWG/Observatory/POLAR`, named `Polar`; the only other
  Polar observatory row is the CDPP-AMDA mirror `CNES/Observatory/CDPP-AMDA/POLAR` under the different
  name "Polar Plasma Laboratory", which the agency-mirror rule excludes. Polar is additionally
  project-asserted: the Zenodo keyword list includes `POLAR`, and `polar` is a stored Field 16 keyword.
- **`Spherical Elementary Current Systems`** — `projects/secs/` is a full plug-in
  (`secs_load_data.pro`, `sec_read_ascii_data.pro`, `eic_ascii2tplot.pro`,
  `secs_read_stations.pro`, `secs_stations2tplot.pro`, `eics_overlay_plots.pro`,
  `seca_overlay_plots.pro`, plus `spedas_gui/plugins/secs_plugin.txt` and the
  `spedas_gui/Resources/secs_mosaic_key.png` / `seca_mosaic_key.png` legends). SPASE models SECS as a
  *virtual* observatory — "the collection of magnetometer arrays used in the creation of the SECS
  datasets… CANMOS, CARISMA, DMI (in Greenland), GIMA, MACCS, THEMIS, STEP" — and as a matching virtual
  instrument, so the association belongs at both levels; the instrument row
  `SMWG/Instrument/SECS/Magnetometer` is recorded in Field 31 with the code evidence for what SPEDAS
  actually reads.
- **`Cassini Orbiter`** and **`Juno Orbiter`** — the das2-based loaders cited under Field 31. Both
  are in `projects/` as ordinary support code, not in an `examples/` directory.
- **`Solar and Heliospheric Observatory`**, **`Explorer 50`** (IMP 8) and **`ISTP/Equator-S`** — the
  legacy ISTP key-parameter loaders `general/key_param/load_so_{cel,cst,ern}.pro`,
  `load_i8_{mag,pla}.pro` and `load_eq_pp_{aux,ici,mam}.pro`. Recorded because dedicated
  per-instrument routines for these missions are genuinely shipped in 6.1, with the caveat already
  stated in Field 31 that they are 1999-era readers expecting locally staged master-index files.
  Equator-S is additionally project-asserted: the Zenodo keyword list includes `EQUATOR-S`.
- **`SuperDARN`** — `projects/erg/ground/radar/superdarn/` with `erg_load_sdfit.pro`,
  `get_scan_struc_arr.pro`, `overlay_map_sdfit.pro`, `overlay_map_sdfov.pro`,
  `get_sd_lat_profile.pro`, `make_fanplot_pictures.pro` and a dedicated colour table. Exactly one
  vocabulary row is named `SuperDARN`, so resolution is unambiguous.
- **The four THEMIS ground-network rows** — `NASA THEMIS GBO Ground Stations`,
  `NASA THEMIS EPO Ground Stations`, `Canadian Magnetometer Array` and
  `NASA THEMIS Ground Stations in Alaska`. Justified by `projects/themis/ground/thm_load_gmag.pro`,
  `thm_load_gmag_networks.pro`, `thm_gmag_stations.pro`, `thm_asi_stations.pro`, `thm_load_asi.pro`,
  `thm_load_ask.pro`, and the shipped station tables `gmag_stations.txt`,
  `GMAG-Station-Code-19700101.txt` and the dated `THEMIS_GMAG_Station_List_*.xlsx` files. Each of the
  four names resolves to exactly one row. This is the network-level granularity the Field 31
  bounding rule chose over expanding to the dozens of per-station rows.
- **`Advanced TIROS-N` (NOAA-18) and `NOAA-N Prime` (NOAA-19)** — the two POES spacecraft
  `poes_load_data.pro` names explicitly. Note that `SMWG/Observatory/NOAA/{16,17,18}` all carry the
  name `Advanced TIROS-N`; that is three *different* spacecraft sharing a name, not an ambiguity,
  and selection is by identifier.
- **The ten GOES spacecraft rows, GOES 8 through 17** — from `goes_load_data.pro`'s documented
  "valid for GOES 08-15" plus `goesr_load_data.pro`'s "GOES-16, GOES-17". The GOES 8–12 rows carry
  COSPAR designations as names (`1994-022A`, `1995-025A`, `1997-019A`, `2000-022A`, `2001-031A`)
  rather than readable titles; those are the canonical row names and are copied verbatim rather than
  improved, because the name must match the row. These per-satellite rows also carry the GOES-16/17
  EXIS and SEISS support that has no instrument row, per the instrument→observatory fallback. The
  broad `Geostationary Operational Environmental Satellites` row already stored is retained
  alongside them.

- **`Canadian Array for Realtime Investigations of Magnetic Activity`** (CARISMA) —
  `projects/themis/ground/thm_load_carisma_gmag.pro` is dedicated support for the Canadian Array for
  Realtime Investigations of Magnetic Activity, with its own 23-site station list (`anna back cont
  daws eski fchp fchu gull isll lgrr mcmu mstk norm osak oxfo pols rabb sach talo thrf vulc weyb
  wgry`) and its own download path: the header states that CARISMA data "is not mirrored by THEMIS.
  The data is downloaded directly from CARISMA (UAlberta) to the user's computer."
- **`British Antarctic Survey`** — `projects/bas/` (`bas_load_data.pro`, `bas_read_data.pro`,
  `bas_get_filename.pro`, `bas_init.pro`, and the shipped file list `lpm_list.txt`) plus
  `projects/themis/ground/thm_load_bas_gmag.pro`.

**How CARISMA and BAS were resolved — a reusable rule, because both looked like SPASE ambiguities and
neither was one.** Each entry matched several same-named `type = 2` rows, and nothing in the SPEDAS
tree broke the tie. The tie-breaker was not in the source tree at all; it was in the **upstream SPASE
records**, and the general rule is worth stating plainly for reuse:

> Among same-named candidate rows, prefer the SPASE ID that no other record names as its `PriorID`.
> Consult the upstream SPASE record's `PriorID` and `ResourceName` before concluding an ambiguity is
> unresolvable.

Applied to the two cases:

- **CARISMA — three candidate rows, resolved to `Ground/CARISMA` on supersession plus positive
  exclusion.** The candidates were `SMWG/Observatory/CARISMA`, `SMWG/Observatory/Ground/CARISMA` and
  `SMWG/Observatory/Ground/CANOPUS`, all `SMWG` and all displaying the same name, so the SMWG
  tie-breaker was useless. Upstream settles it twice over. First, supersession:
  `spase://SMWG/Observatory/Ground/CARISMA` declares `PriorID = spase://SMWG/Observatory/CARISMA`, so
  the `Ground/` form is the **current** identifier and the bare form is the **superseded** one.
  Locally corroborated: of the three rows, `Ground/CARISMA` is the only one carrying a `landing_url`
  (`https://helio.data.nasa.gov/mission/Ground_CARISMA`). Second, entity separation: upstream
  `ResourceName` distinguishes the resources — `Ground/CARISMA` is named `CARISMA`, while
  `Ground/CANOPUS` is named `CANOPUS` and declares no `PriorID`. They are different resources, not two
  identifiers for one. CANOPUS is then excluded on **positive** evidence rather than by guess:
  `grep -ril canopus` over the whole archive returns zero hits, while `carisma` returns seven files.
  SPEDAS supports CARISMA and says nothing about its CANOPUS predecessor.
- **BAS — two candidate rows, resolved to `Ground/BAS`, with no wrong-entity risk at all.**
  `spase://SMWG/Observatory/Ground/BAS` declares `PriorID = spase://SMWG/Observatory/BAS`, and both
  records carry `ResourceName = British Antarctic Survey`. This is genuinely one resource under an old
  and a new identifier, so the only exposure was recording a stale identifier, never the wrong entity.

**A durable upstream/ingest defect behind the CARISMA collision — recorded because it will look like a
data error to a future reader.** The three CARISMA-family rows collided in HSSI only because of an
ingest artifact, not because SPASE is ambiguous. `Ground/CARISMA`'s SPASE record carries
`ResourceName = CARISMA` plus three `AlternateName` elements, the third being
`Canadian Auroral Network for the OPEN (Origins of Plasmas in Earth°s Neighborhood) Program Unified
Study`. HSSI ingested that **third alternate name instead of `ResourceName`**, splitting it on the
parenthesis into a name (`Canadian Auroral Network for the OPEN`) plus an abbreviation
(`Origins of Plasmas in Earth°s Neighborhood`) and dropping the trailing `Program Unified Study`.
Because all three rows carried that same alternate name, all three displayed CANOPUS's formal name —
which is what made them look indistinguishable.

Three consequences worth carrying forward. The SPEDAS entry **displayed** as
`Canadian Auroral Network for the OPEN` for as long as the row carried that name — a name that was not
merely cosmetically wrong but named the wrong network, CANOPUS being CARISMA's predecessor, while the
association itself was correct throughout. The canonical relationship must retain the vocabulary row's
exact name and SPASE identifier rather than substituting the free text `CARISMA`. Correcting the
display required a catalogue vocabulary refresh from upstream SPASE metadata, and that refresh has
since happened: the row now carries the correct expansion of CARISMA,
`Canadian Array for Realtime Investigations of Magnetic Activity`, with abbreviation `CARISMA`, and
that is the name recorded in Field 32 above. The relationship itself never changed — same row, same
`Ground/CARISMA` identifier, same evidence.

**One caveat outlives the correction.** The maintained upstream registry's own `long_name` for this
observatory still carries the defective CANOPUS-fragment form, so a future vocabulary refresh may
transiently reinstate `Canadian Auroral Network for the OPEN` on this row until the upstream record is
fixed. The identifier `https://spase-metadata.org/SMWG/Observatory/Ground/CARISMA` and the reasoning
recorded here are the durable halves of this entry; the stored name is the fragile half. If the wrong
name reappears it should be re-corrected against the SPASE record's `ResourceName` and
`AlternateNames`, not re-adopted as though it were the row's true name.

One trap inside that trap: the `Earth°s` mojibake is **upstream in SPASE itself** — the
`Ground/CARISMA` and `Ground/CANOPUS` XML literally contain `Earth°s` — not an HSSI transcription
error. The superseded bare `Observatory/CARISMA` record happens to carry the correctly-typeset
`Earth’s` in the same alternate name, and its HSSI row reflected that faithfully. That cosmetic
advantage is **not** a reason to prefer the superseded row: `PriorID` governs, and HSSI transcribed
both records accurately.

**No entry in this field is ambiguous either.** CARISMA and BAS, the two entries that once were, are
resolved above, and every value carries an `https://spase-metadata.org/` identifier.

**Observatories considered and not recorded** — beyond the Field 31 omissions, which apply here too
(Solar Orbiter, IMAGE, MetOp, Galileo, and the *station-level* rows of the ground networks, whose
network-level rows are recorded above where the vocabulary offers them): **GEO-KOMPSAT-2A** is an
omission of the same kind, for the reason given with the `KOMPSAT` removal — SOSMAG support is real but
no GK2A row exists at any level. `Lomonosov`, `LuSEE`, `SWFO` and `ESCAPADE` have real plug-ins
(`projects/lomonosov/`, `projects/lusee/`, `projects/SWFO/`, `projects/escapade/`) but **no observatory
row at any path** in the vocabulary, so there is nothing to resolve to; each is a documented omission
awaiting an upstream heliophysics.net/SPASE refresh. `IUGONET` likewise has no observatory row of its
own — it is a data-network programme rather than an observatory, and its member instruments appear only
as station-level `IUGONET/Observatory/...` rows.

Polar is **not** among these omissions; it is recorded above at observatory level and in Field 31 at
instrument level, where the false premise that no Polar row exists is set out and refuted.

### 33. Logo (OPTIONAL)
Not found — no logo exists at a permanent, publicly accessible URL.

**HSSI stored an empty string, and after a full search it should stay empty.** This is a documented
negative result. Four places were checked:

- **`https://spedas.org/`** — the project home page (a WordPress site) contains **no `<img>` elements
  at all** and no reference to a logo file anywhere in its markup.
- **`https://spedas.org/wiki`** — the MediaWiki instance uses no site logo. The only images on
  `Main_Page` are `Spedas_overview_d.png`, which its own caption identifies as a screenshot of the
  "SPEDAS Graphical User Interface", and the generic `poweredby_mediawiki_88x31.png` badge. A GUI
  screenshot is not a logo.
- **The 6.1 source tree — a project logo does exist here, and this is the one place worth being
  precise about.** `spedas_gui/Resources/` holds 50 entries. Most are user-interface icons
  (`arrow_*.bmp`, `magnifier_zoom.bmp`, `disk.bmp`, `printer.bmp`, …) and plot colour-bar legends
  (`goes10-12key.png`, `goes13-15key.png`, `poes_key.png`, `secs_mosaic_key.png`,
  `seca_mosaic_key.png`, `secs_quicklook_key.png`, `overplotkey.png`) — but two are genuine logos:
  **`spedas_gui/Resources/spedas_logo.bmp`**, a 135×135 24-bit Windows bitmap that
  `spedas_gui/spd_gui.pro` line 1404 loads as the GUI's palette/window icon
  (`palettebmp = read_bmp(rpath + 'spedas_logo.bmp', /rgb)`), and `thmLogo.bmp`, a 64×64 THEMIS logo
  that `projects/mms/sitl/eva/eva.pro` line 98 loads the same way. What Field 33 asks for, though, is
  a permanent publicly accessible URL, and neither bitmap has one — both exist only inside the release
  archive, at no addressable location — so neither can populate this field. A future refresh should
  not read "a logo exists" as "Field 33 is fillable"; it would become fillable only if the project
  published the bitmap at a stable URL.
- **The Zenodo deposit** — record 15023025 contains exactly one file, `spedas_6_1.zip`; there is no
  logo or thumbnail asset.

No URL is recorded, because inventing one or pointing at a screenshot would be worse than an honest
empty value.

---

## Agreement

### Metadata Agreement (MANDATORY)
Agreed — this metadata is drawn from the software's own release archive, its official documentation
wiki, and its published DOI metadata, and is contributed for inclusion in HSSI.
