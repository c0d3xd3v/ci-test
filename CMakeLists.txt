cmake_minimum_required(VERSION 3.14)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(CMAKE_USER_MAKE_RULES_OVERRIDE
  ${CMAKE_CURRENT_SOURCE_DIR}/cmake/c_flag_overrides.cmake)
set(CMAKE_USER_MAKE_RULES_OVERRIDE_CXX
  ${CMAKE_CURRENT_SOURCE_DIR}/cmake/cxx_flag_overrides.cmake)


project(ci-test VERSION 0.1 LANGUAGES CXX)


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


include(ExternalProject) 

ExternalProject_Add(gmp
    GIT_REPOSITORY https://github.com/gx/gmp.git
	GIT_TAG 6.1.2-2
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
	-DCMAKE_MSVC_RUNTIME_LIBRARY="MultiThreaded$<$<CONFIG:Release>:Release>"
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

SET(GMP_WINDOWS_PATH "C:/Program Files (x86)/GMP/")

##ExternalProject_Add(fTetWild
#    GIT_REPOSITORY https://github.com/c0d3xd3v/fTetWild.git
#	GIT_TAG        patch-1
#	DEPENDS gmp
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
#    CMAKE_ARGS
#	-DCMAKE_MSVC_RUNTIME_LIBRARY="MultiThreaded$<$<CONFIG:Release>:Release>"
#	-DGMP_LIBRARIES="C:/Program Files (x86)/GMP/lib"
#	-DGMP_DIR="C:/Program Files (x86)/GMP/lib/cmake/gmp"
#    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
#)

