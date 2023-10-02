cmake_minimum_required(VERSION 3.14)

project(ci-test VERSION 0.1 LANGUAGES CXX)


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

include(ExternalProject) 

ExternalProject_Add(gmp
    GIT_REPOSITORY https://github.com/gx/gmp.git
	GIT_TAG 6.1.2-2
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

SET(GMP_WINDOWS_PATH "C:/Program Files (x86)/GMP/")

ExternalProject_Add(fTetWild
    GIT_REPOSITORY https://github.com/c0d3xd3v/fTetWild.git
	GIT_TAG        patch-1
	DEPENDS gmp
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
	-DCMAKE_CXX_FLAGS="/p:Platform=x64 /p:NODEFAULTLIB=msvcprt.lib /p:RuntimeLibrary=MT_StaticRelease"
	-DGMP_LIBRARIES="C:/Program Files (x86)/GMP/lib"
	-DGMP_DIR="C:/Program Files (x86)/GMP/lib/cmake/gmp"
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

