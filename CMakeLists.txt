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

#ExternalProject_Add(cli11
#    GIT_REPOSITORY https://github.com/CLIUtils/CLI11.git
#    GIT_TAG v1.8.0
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    CMAKE_ARGS
#    -DBUILD_TESTING=OFF
#    -DBUILD_EXAMPLES=OFF
#    -DBUILD_EXAMPLES_JSON=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

#ExternalProject_Add(tbb
#    GIT_REPOSITORY https://github.com/wjakob/tbb.git
#    GIT_TAG ddbe45cd3ad89df9a84cd77013d5898fc48b8e89
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    CMAKE_ARGS
#    -DTBB_BUILD_TESTS=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

#ExternalProject_Add(fmt
#    GIT_REPOSITORY https://github.com/fmtlib/fmt.git
#    GIT_TAG 5.3.0
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    CMAKE_ARGS
#    -DFMT_TEST=OFF
#    -DFMT_CUDA_TEST=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

#ExternalProject_Add(spdlog
#    GIT_REPOSITORY https://github.com/gabime/spdlog.git
#    GIT_TAG v1.3.1
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    CMAKE_ARGS
#    -DSPDLOG_BUILD_BENCH=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

#ExternalProject_Add(eigen
#    GIT_REPOSITORY https://gitlab.com/libeigen/eigen.git
#    GIT_TAG 3.4.1
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    CMAKE_ARGS
#    -DEIGEN_BUILD_TESTING=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

#ExternalProject_Add(geogram
#    GIT_REPOSITORY https://github.com/polyfem/geogram.git
#    #GIT_TAG b613750341a6cdd31ae8df80ecfc26ac7ca1a6ad
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    CMAKE_ARGS
#    -DVORPALINE_ARCH_64=TRUE
#    -DVORPALINE_BUILD_DYNAMIC=FALSE
#    -DGEOGRAM_WITH_GRAPHICS=OFF
#    -DGEOGRAM_WITH_LEGACY_NUMERICS=OFF
#    -DGEOGRAM_WITH_HLBFGS=OFF
#    -DGEOGRAM_WITH_TETGEN=OFF
#    -DGEOGRAM_WITH_TRIANGLE=OFF
#    -DGEOGRAM_WITH_EXPLORAGRAM=OFF
#    -DGEOGRAM_WITH_LUA=OFF
#    -DGEOGRAM_LIB_ONLY=ON
#    -DGEOGRAM_WITH_FPG=OFF
#    -DGEOGRAM_USE_SYSTEM_GLFW3=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

#ExternalProject_Add(igl
#    GIT_REPOSITORY https://github.com/libigl/libigl.git
#    GIT_TAG v2.5.0
#    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#    DEPENDS eigen gmp
#    CMAKE_ARGS
#    -DGMP_DIR=${CMAKE_INSTALL_PREFIX}/3rdparty/lib/cmake/gmp
#    -DLIBIGL_USE_STATIC_LIBRARY=OFF
#    -DLIBIGL_WITH_COMISO=OFF
#    -DLIBIGL_EMBREE=OFF
#    -DLIBIGL_OPENGL=OFF
#    -DLIBIGL_GLFW_TESTS=OFF
#    -DLIBIGL_WITH_OPENGL_GLFW=OFF
#    -DLIBIGL_WITH_OPENGL_GLFW_IMGUI=OFF
#    -DLIBIGL_WITH_PNG=OFF
#    -DLIBIGL_WITH_TETGEN=OFF
#    -DLIBIGL_WITH_TRIANGLE=OFF
#    -DLIBIGL_PREDICATES=ON
#    -DLIBIGL_XML=OFF
#    -DLIBIGL_BUILD_TESTS=OFF
#    -DLIBIGL_BUILD_TUTORIALS=OFF
#    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

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

# ExternalProject_Add(zlib
#     GIT_REPOSITORY https://github.com/zlib-ng/zlib-ng.git
#     GIT_TAG 2.1.4
#     INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
#     CMAKE_ARGS
#     -DZLIB_COMPAT=ON
#     -DZLIB_ENABLE_TESTS=OFF
#     -DWITH_GTEST=OFF
#     -DWITH_BENCHMARKS=OFF
#     -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty
#)

ExternalProject_Add(ngsolve
    GIT_REPOSITORY https://github.com/NGSolve/ngsolve.git
    GIT_TAG v6.2.2305
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty/ngsolve
#    DEPENDS zlib
    CMAKE_ARGS
    -DUSE_CUDA=OFF
    -DCMAKE_BUILD_TYPE=RELEASE
    -DADDITIONAL_PATHS=${CMAKE_INSTALL_PREFIX}/3rdparty
#    -DUSE_GUI=OFF
#    -DZLIB_INCLUDE_DIR=${CMAKE_INSTALL_PREFIX}/3rdparty/include/
#    -DZLIB_LIBRARY=${CMAKE_INSTALL_PREFIX}/3rdparty/lib/
    #-DINSTALL_DEPENDENCIES=ON
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/3rdparty/ngsolve
)

ExternalProject_Add(vtk
    GIT_REPOSITORY https://gitlab.kitware.com/vtk/vtk.git
    GIT_TAG v9.2.6
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/3rdparty
    CMAKE_ARGS
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

ExternalProject_Add(app
    GIT_REPOSITORY https://github.com/c0d3xd3v/NGSovleCoding.git
    GIT_TAG main
    DEPENDS fTetWild vtk ngsolve
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}/app
    SOURCE_DIR C++/
    CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}/app
)
# find_package(Qt5 REQUIRED COMPONENTS Quick QuickControls2 Gui)
# 
# add_executable(test_bin test/main.cpp)
# 
# target_link_directories(test_bin PUBLIC "${CMAKE_INSTALL_PREFIX}/3rdparty/lib/")
# target_link_directories(test_bin PUBLIC "${CMAKE_INSTALL_PREFIX}/3rdparty/ngsolve/lib/")
# target_link_libraries(test_bin
#     Qt5::Gui
#     Qt5::Quick
#     FloatTetwild
#     FastEnvelope
#     nglib
#     ngcore
#     libngsolve
# )
# 
# install(TARGETS test_bin
#         CONFIGURATIONS Release
#         RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/3rdparty/bin/")
