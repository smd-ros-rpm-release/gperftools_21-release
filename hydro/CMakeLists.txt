cmake_minimum_required(VERSION 2.8.3)
project(gperftools)

find_package(catkin REQUIRED)

include(ExternalProject)

ExternalProject_Add(gperftools
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}
  CONFIGURE_COMMAND touch ${CMAKE_CURRENT_SOURCE_DIR}/aclocal.m4 ${CMAKE_CURRENT_SOURCE_DIR}/Makefile.in && ${CMAKE_CURRENT_SOURCE_DIR}/configure --prefix=${CMAKE_INSTALL_PREFIX}
  BUILD_COMMAND make
  INSTALL_COMMAND ""
  )
ExternalProject_Get_Property(gperftools BINARY_DIR)

# TODO: extras to export the GPERFTOOLS_TCMALLOC, GPERFTOOLS_PROFILER, and GPERFTOOLS tcmalloc_and_profiler
# variables
catkin_package(
  INCLUDE_DIRS src
  CFG_EXTRAS gperftools-extras.cmake
  )


message("gperftools binary dir: ${BINARY_DIR}")
install(CODE
  "execute_process(COMMAND make -C ${BINARY_DIR} install)"
  )

install(FILES cmake/gperftools-extras.cmake
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/cmake)
