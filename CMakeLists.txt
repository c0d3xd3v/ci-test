cmake_minimum_required(VERSION 3.14)

project(ci-test VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Quick)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Quick)


list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

include(ExternalProject) 

ExternalProject_Add(gmp
    GIT_REPOSITORY https://github.com/gx/gmp.git
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

ExternalProject_Add(fTetWild
    GIT_REPOSITORY https://github.com/wildmeshing/fTetWild
	GIT_TAG         f471f09dd26006745387dd61694762f861c787b9
    INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
    CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

set(PROJECT_SOURCES
        main.cpp
        qml.qrc
)

add_executable(ci-test ${PROJECT_SOURCES})
target_link_libraries(ci-test
  PRIVATE Qt${QT_VERSION_MAJOR}::Core Qt${QT_VERSION_MAJOR}::Quick)
