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
	#CMAKE_GENERATOR "Visual Studio 16 2019 Win64"
    CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

##ExternalProject_Add(fTetWild
#    GIT_REPOSITORY https://github.com/wildmeshing/fTetWild
#	GIT_TAG         f471f09dd26006745387dd61694762f861c787b9
#	DEPENDS gmp
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
#    CMAKE_ARGS
#    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
#)

