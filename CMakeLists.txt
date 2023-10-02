cmake_minimum_required(VERSION 3.14)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(CMAKE_USER_MAKE_RULES_OVERRIDE ${CMAKE_CURRENT_SOURCE_DIR}/cmake/c_flag_overrides.cmake)
set(CMAKE_USER_MAKE_RULES_OVERRIDE_CXX ${CMAKE_CURRENT_SOURCE_DIR}/cmake/cxx_flag_overrides.cmake)

project(ci-test VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(ExternalProject) 

ExternalProject_Add(gmp
    GIT_REPOSITORY https://github.com/gx/gmp.git
	GIT_TAG 6.1.2-2
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
)

ExternalProject_Add(cli11
    GIT_REPOSITORY https://github.com/CLIUtils/CLI11.git
	GIT_TAG v1.8.0
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
)

ExternalProject_Add(tbb
    GIT_REPOSITORY https://github.com/wjakob/tbb.git
	GIT_TAG ddbe45cd3ad89df9a84cd77013d5898fc48b8e89
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
)

ExternalProject_Add(fmt
    GIT_REPOSITORY https://github.com/fmtlib/fmt.git
	GIT_TAG 5.3.0
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
)

ExternalProject_Add(spdlog
    GIT_REPOSITORY https://github.com/gabime/spdlog.git
	GIT_TAG v1.3.1
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
)

ExternalProject_Add(geogram
    GIT_REPOSITORY https://github.com/polyfem/geogram.git
	#GIT_TAG b613750341a6cdd31ae8df80ecfc26ac7ca1a6ad
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
)

#SET(GMP_WINDOWS_PATH "C:/Program Files (x86)/GMP/")

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

