cmake_minimum_required(VERSION 2.8.3)
include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.23.182.tar.gz"
    SHA1 "951072d4aafac23473f072a0cb3119020b36a943"
)

project(genmsg)

hunter_add_package(catkin)

find_package(catkin REQUIRED)

catkin_package(CFG_EXTRAS genmsg-extras.cmake)

install(
  FILES
  cmake/pkg-genmsg.cmake.em
  cmake/pkg-genmsg.context.in
  cmake/pkg-msg-extras.cmake.in
  cmake/pkg-msg-paths.cmake.develspace.in
  cmake/pkg-msg-paths.cmake.installspace.in
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/cmake)

catkin_python_setup()

install(
  PROGRAMS scripts/genmsg_check_deps.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

if(CATKIN_ENABLE_TESTING)
  catkin_add_nosetests(test)
endif()
