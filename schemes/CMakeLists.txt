# Set default project to unknown
if(NOT PROJECT)
  message(STATUS "Setting CCPP project to 'unknown' as none was specified.")
  set(PROJECT "Unknown")
endif (NOT PROJECT)

#------------------------------------------------------------------------------
# Include the external test project only in standalone builds (project not set)
#------------------------------------------------------------------------------
if (PROJECT STREQUAL "Unknown")
  include(ExternalProject)

  #----------------------------------------------------------------------------
  # The checker scheme
  ExternalProject_Add(
      check
      DEPENDS ccpp
      SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/check"
      PREFIX "check"
      DOWNLOAD_COMMAND  ""
      UPDATE_COMMAND    ""
      INSTALL_COMMAND   ""
      CMAKE_ARGS -DCCPP_INCLUDE_DIRS=${CCPP_INCLUDE_DIRS}
                 -DCCPP_LIB_DIRS=${CCPP_LIB_DIRS}
                 -DPROJECT=${PROJECT}
                 -DCMAKE_Fortran_FLAGS=${CMAKE_Fortran_FLAGS}
                 -DCMAKE_SHARED_LIBRARY_CREATE_Fortran_FLAGS=${CMAKE_SHARED_LIBRARY_CREATE_Fortran_FLAGS}
                 -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
  )
endif (PROJECT STREQUAL "Unknown")