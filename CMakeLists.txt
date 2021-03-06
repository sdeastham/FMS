esma_set_this ()
string (REPLACE fms_ "" precision ${this})

# The following logic is to avoid duplication in the supported GNUMake logic.
# Source files (and headers) are listed in a separate file, and we must
# process this into something that CMake can use for assembling a library.


set(srcs_and_includes
  amip_interp/amip_interp.F90
  astronomy/astronomy.F90
  axis_utils/axis_utils.F90
  column_diagnostics/column_diagnostics.F90
  constants/constants.F90
  coupler/atmos_ocean_fluxes.F90
  coupler/coupler_types.F90
  coupler/ensemble_manager.F90
  data_override/data_override.F90
  diag_manager/diag_axis.F90
  diag_manager/diag_data.F90
  diag_manager/diag_grid.F90
  diag_manager/diag_manager.F90
  diag_manager/diag_output.F90
  diag_manager/diag_util.F90
  drifters/cloud_interpolator.F90
  drifters/drifters_comm.F90
  drifters/drifters_compute_k.h
  drifters/drifters_core.F90
  drifters/drifters.F90
  drifters/drifters_input.F90
  drifters/drifters_io.F90
  drifters/drifters_push.h
  drifters/drifters_set_field.h
  drifters/fms_switches.h
  drifters/quicksort.F90
  exchange/stock_constants.F90
  exchange/xgrid.F90
  fft/fft99.F90
  fft/fft.F90
  field_manager/field_manager.F90
  field_manager/fm_util.F90
  field_manager/parse.inc
  fms/fms.F90
  fms/fms_io.F90
  fms/read_data_2d.inc
  fms/read_data_3d.inc
  fms/read_data_4d.inc
  fms/test_fms_io.F90
  fms/write_data.inc
  horiz_interp/horiz_interp_bicubic.F90
  horiz_interp/horiz_interp_bilinear.F90
  horiz_interp/horiz_interp_conserve.F90
  horiz_interp/horiz_interp.F90
  horiz_interp/horiz_interp_spherical.F90
  horiz_interp/horiz_interp_type.F90
  include/fms_platform.h
  memutils/memuse.c
  memutils/memutils.F90
  mosaic/constant.h
  mosaic/create_xgrid.c
  mosaic/create_xgrid.h
  mosaic/gradient_c2l.c
  mosaic/gradient_c2l.h
  mosaic/gradient.F90
  mosaic/grid.F90
  mosaic/interp.c
  mosaic/interp.h
  mosaic/mosaic.F90
  mosaic/mosaic_util.c
  mosaic/mosaic_util.h
  mosaic/read_mosaic.c
  mosaic/read_mosaic.h
  mpp/include/mpp_chksum.h
  mpp/include/mpp_chksum_int.h
  mpp/include/mpp_chksum_scalar.h
  mpp/include/mpp_comm.inc
  mpp/include/mpp_comm_mpi.inc
  mpp/include/mpp_comm_nocomm.inc
  mpp/include/mpp_comm_sma.inc
  mpp/include/mpp_data_mpi.inc
  mpp/include/mpp_data_nocomm.inc
  mpp/include/mpp_data_sma.inc
  mpp/include/mpp_do_check.h
  mpp/include/mpp_do_checkV.h
  mpp/include/mpp_do_get_boundary.h
  mpp/include/mpp_do_global_field.h
  mpp/include/mpp_domains_comm.inc
  mpp/include/mpp_domains_define.inc
  mpp/include/mpp_domains_misc.inc
  mpp/include/mpp_domains_reduce.inc
  mpp/include/mpp_domains_util.inc
  mpp/include/mpp_do_redistribute.h
  mpp/include/mpp_do_update_ad.h
  mpp/include/mpp_do_update.h
  mpp/include/mpp_do_updateV_ad.h
  mpp/include/mpp_do_updateV.h
  mpp/include/mpp_error_a_a.h
  mpp/include/mpp_error_a_s.h
  mpp/include/mpp_error_s_a.h
  mpp/include/mpp_error_s_s.h
  mpp/include/mpp_get_boundary.h
  mpp/include/mpp_global_field.h
  mpp/include/mpp_global_reduce.h
  mpp/include/mpp_global_sum_ad.h
  mpp/include/mpp_global_sum.h
  mpp/include/mpp_global_sum_tl.h
  mpp/include/mpp_io_connect.inc
  mpp/include/mpp_io_misc.inc
  mpp/include/mpp_io_read.inc
  mpp/include/mpp_io_util.inc
  mpp/include/mpp_io_write.inc
  mpp/include/mpp_read_2Ddecomp.h
  mpp/include/mpp_reduce_mpi.h
  mpp/include/mpp_reduce_nocomm.h
  mpp/include/mpp_reduce_sma.h
  mpp/include/mpp_sum.inc
  mpp/include/mpp_sum_mpi.h
  mpp/include/mpp_sum_nocomm.h
  mpp/include/mpp_sum_sma.h
  mpp/include/mpp_transmit.inc
  mpp/include/mpp_transmit_mpi.h
  mpp/include/mpp_transmit_nocomm.h
  mpp/include/mpp_transmit_sma.h
  mpp/include/mpp_update_domains2D_ad.h
  mpp/include/mpp_update_domains2D.h
  mpp/include/mpp_util.inc
  mpp/include/mpp_util_mpi.inc
  mpp/include/mpp_util_nocomm.inc
  mpp/include/mpp_util_sma.inc
  mpp/include/mpp_write_2Ddecomp.h
  mpp/include/mpp_write.h
  mpp/include/system_clock.h
  mpp/mpp_data.F90
  mpp/mpp_domains.F90
  mpp/mpp.F90
  mpp/mpp_io.F90
  mpp/mpp_memutils.F90
  mpp/mpp_parameter.F90
  mpp/mpp_pset.F90
  mpp/mpp_utilities.F90
  mpp/mpp_efp.F90
  mpp/nsclock.c
  mpp/test_mpp_domains.F90
  mpp/test_mpp.F90
  mpp/test_mpp_io.F90
  mpp/test_mpp_pset.F90
  mpp/threadloc.c
  oda_tools/oda_core.F90
  oda_tools/oda_types.F90
  oda_tools/write_ocean_data.F90
  oda_tools/xbt_drop_rate_adjust.f90
  platform/platform.F90
  random_numbers/MersenneTwister.F90
  random_numbers/random_numbers.F90
  sat_vapor_pres/sat_vapor_pres.F90
  sat_vapor_pres/sat_vapor_pres_k.F90
  station_data/station_data.F90
  time_interp/time_interp_external.F90
  time_interp/time_interp.F90
  time_manager/get_cal_time.F90
  time_manager/time_manager.F90
  topography/gaussian_topog.F90
  topography/topography.F90
  tracer_manager/tracer_manager.F90
  tridiagonal/tridiagonal.F90
  mpp/include/mpp_do_update_nest.h                
  mpp/include/mpp_gather.h                        
  mpp/include/mpp_define_nest_domains.inc         
  mpp/include/mpp_update_nest_domains.h           
  mpp/include/mpp_do_update_nonblock.h            
  mpp/include/mpp_do_updateV_nonblock.h           
  mpp/include/mpp_update_domains2D_nonblock.h     
  exchange/test_xgrid.F90                         
  diag_manager/diag_table.F90                     
  diag_manager/diag_manifest.F90
  )


# Filter out header files
set (srcs)
foreach (file ${srcs_and_includes})
  string (REGEX MATCH ".+\\.h" header ${file})
  string (REGEX MATCH ".+\\.inc" inc ${file})
  if (header OR inc)
  else ()
    list (APPEND srcs ${file})
  endif ()
endforeach ()

set (lib fms_${precision})

esma_add_library (${lib} SRCS ${srcs})
# GCHP: change linked libraries
#target_link_libraries (${lib} ${NETCDF_LIBRARIES} ${MPI_Fortran_LIBRARIES})
target_link_libraries (${lib} ${NETCDF_LIBRARIES} MPI::MPI_Fortran)

target_include_directories (${lib} PUBLIC include mpp/include fft fms)
target_include_directories (${lib} PUBLIC ${INC_NETCDF})

file (COPY include/fms_platform.h DESTINATION ${include_${this}})
file (COPY include/file_version.h DESTINATION ${include_${this}})

# Various compiler options and CPP definitions ...
target_compile_definitions (${lib} PRIVATE OVERLOAD_R4 MAPL_MODE SPMD use_libMPI use_netCDF PORTABLE_KINDS)

if (APPLE)
   target_compile_definitions(${lib} PRIVATE __APPLE__)
endif ()

set (CMAKE_Fortran_FLAGS_RELEASE "${GEOS_Fortran_FLAGS_VECT}")

if (CMAKE_Fortran_COMPILER_ID MATCHES "NAG")
  target_compile_options (${lib} PRIVATE $<$<COMPILE_LANGUAGE:Fortran>:-kind=byte>)
endif ()
if (CMAKE_Fortran_COMPILER_ID MATCHES "GNU")
  target_compile_options (${lib} PRIVATE $<$<COMPILE_LANGUAGE:Fortran>:-fcray-pointer>)
endif ()
if (CMAKE_Fortran_COMPILER_ID MATCHES "Intel")
  target_compile_options (${lib} PRIVATE $<$<COMPILE_LANGUAGE:Fortran>:-diag-disable 6843,7712>) # warnings about dummy args
endif ()
if (CMAKE_Fortran_COMPILER_ID MATCHES "PGI")
  target_compile_definitions (${lib} PRIVATE NO_QUAD_PRECISION)
endif ()

if (precision MATCHES "r8")
  esma_fortran_generator_list(${lib} ${FREAL8})
endif ()





  
