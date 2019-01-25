cmake_minimum_required(VERSION 2.6.2)

project( googletest-distribution )

enable_testing()

option(BUILD_GTEST "Builds the googletest subproject" OFF)
option(GTEST_MOCK_FS "Disable filesystem calls" OFF)

if(GTEST_MOCK_FS)
  add_definitions(-DGTEST_HAS_POSIX_RE=0)
  add_definitions(-DGTEST_HAS_STREAM_REDIRECTION=0)
  add_definitions(-DGTEST_MOCK_FS=1)
endif()

#Note that googlemock target already builds googletest
option(BUILD_GMOCK "Builds the googlemock subproject" ON)

if(BUILD_GMOCK)
  add_subdirectory( googlemock )
elseif(BUILD_GTEST)
  add_subdirectory( googletest )
endif()
