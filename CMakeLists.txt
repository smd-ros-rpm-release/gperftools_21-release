cmake_minimum_required(VERSION 2.8.3)
project(gperftools)

find_package(catkin REQUIRED)

include(ExternalProject)

ExternalProject_Add(gperftools
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}
  CONFIGURE_COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/configure --prefix=${CMAKE_INSTALL_PREFIX}
  BUILD_COMMAND ${MAKE}
  INSTALL_COMMAND ${MAKE} install
  )

catkin_package(
  )
