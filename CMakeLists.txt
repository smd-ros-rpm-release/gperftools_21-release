cmake_minimum_required(VERSION 2.8.3)
project(gperftools)

find_package(catkin REQUIRED)

include(ExternalProject)

ExternalProject_Add(gperftools
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}
  CONFIGURE_COMMAND touch ${CMAKE_CURRENT_SOURCE_DIR}/aclocal.m4 ${CMAKE_CURRENT_SOURCE_DIR}/Makefile.in && ${CMAKE_CURRENT_SOURCE_DIR}/configure --prefix=${CMAKE_INSTALL_PREFIX}
  BUILD_COMMAND make
  )

catkin_package(
  )
