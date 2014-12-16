cmake_minimum_required(VERSION 2.8.3)
project(gperftools_21)

find_package(catkin REQUIRED)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR}/cmake)
find_package(Gperftools REQUIRED)

catkin_package(
  INCLUDE_DIRS ${GPERFTOOLS_INCLUDE_DIRS}
  CFG_EXTRAS FindGperftools.cmake
)
