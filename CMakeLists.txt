cmake_minimum_required(VERSION 2.8.3)
project(gperftools)

find_package(catkin REQUIRED)

include(ExternalProject)

ExternalProject_Add(gperftools
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}
  CONFIGURE_COMMAND touch ${CMAKE_CURRENT_SOURCE_DIR}/aclocal.m4 ${CMAKE_CURRENT_SOURCE_DIR}/Makefile.in && ${CMAKE_CURRENT_SOURCE_DIR}/configure --prefix=${CMAKE_INSTALL_PREFIX}
  BUILD_COMMAND make
  INSTALL_COMMAND make install prefix=${CATKIN_DEVEL_PREFIX}
  )
ExternalProject_Get_Property(gperftools BINARY_DIR)

# make directory for catkin_package
file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

catkin_package(
  INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
  CFG_EXTRAS gperftools-extras.cmake
  )

message("gperftools binary dir: ${BINARY_DIR}")
install(CODE
  "execute_process(COMMAND make -C ${BINARY_DIR} install)"
  )


