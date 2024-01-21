cmake_minimum_required(VERSION 3.14)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

#set(CMAKE_USER_MAKE_RULES_OVERRIDE ${CMAKE_CURRENT_SOURCE_DIR}/cmake/c_flag_overrides.cmake)
#set(CMAKE_USER_MAKE_RULES_OVERRIDE_CXX ${CMAKE_CURRENT_SOURCE_DIR}/cmake/cxx_flag_overrides.cmake)

project(ci-test VERSION 0.1 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(ExternalProject) 


if (WIN32)
#on linux this should be installed via package manager.
ExternalProject_Add(gmp
    GIT_REPOSITORY https://github.com/gx/gmp.git
    GIT_TAG 6.1.2-2
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
    CMAKE_ARGS
    -DBUILD_TESTING=OFF
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
)
endif(WIN32)

#add_custom_target(my_custom_target
#    COMMAND
#        echo building test
#        cd test
#        mkdir build
#        cd build
#        ${CMAKE_COMMAND} .. -D${GMP_DIR}
#    DEPENDS gmp fmt tbb cli11 geogram igl eigen spdlog
#    VERBATIM
#)

ExternalProject_Add(ngsolve
    GIT_REPOSITORY https://github.com/NGSolve/ngsolve.git
    GIT_TAG v6.2.2305
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty/ngsolve
    CMAKE_ARGS
    -DUSE_CUDA=OFF
    -DCMAKE_BUILD_TYPE=RELEASE
    -DADDITIONAL_PATHS=${CMAKE_INSTALL_PREFIX}/3rdparty
    -DUSE_PYTHON=OFF
    -DUSE_GUI=OFF
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty/ngsolve
)

ExternalProject_Add(vtk
    GIT_REPOSITORY https://gitlab.kitware.com/vtk/vtk.git
    GIT_TAG v9.2.6
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
    CMAKE_ARGS
    -DVTK_BUILD_EXAMPLES:BOOL=OFF
    -DVTK_BUILD_TESTING=OFF
    -DVTK_GROUP_ENABLE_Qt:STRING=YES
    -DVTK_WRAP_PYTHON=OFF
    -DVTK_WRAP_JAVA=OFF
    -DCMAKE_BUILD_TYPE=RELEASE
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
)

ExternalProject_Add(fTetWild
    GIT_REPOSITORY https://github.com/c0d3xd3v/fTetWild.git
    GIT_TAG master
    DEPENDS gmp
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
    CMAKE_ARGS
    #-DBUILD_SHARED_LIBS=ON
    -DGMP_DIR=${CMAKE_INSTALL_PREFIX}/3rdparty/lib/cmake/gmp
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
)

#ExternalProject_Add(app
#    GIT_REPOSITORY https://github.com/c0d3xd3v/NGSovleCoding.git
#    GIT_TAG main
#    DEPENDS fTetWild vtk ngsolve
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/app
#    SOURCE_DIR C++/
#    CMAKE_ARGS
#    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/app
#)
