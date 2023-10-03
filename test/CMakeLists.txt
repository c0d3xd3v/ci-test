 cmake_minimum_required(VERSION 3.14)

set(CMAKE_USER_MAKE_RULES_OVERRIDE ${CMAKE_CURRENT_SOURCE_DIR}/cmake/c_flag_overrides.cmake)
set(CMAKE_USER_MAKE_RULES_OVERRIDE_CXX ${CMAKE_CURRENT_SOURCE_DIR}/cmake/cxx_flag_overrides.cmake)

project(test VERSION 0.1 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(GMP)
find_package(GMPXX)
find_package(TBB)
find_package(fmt)
find_package(spdlog)
find_package(eigen)
find_package(CLI11)
find_package(Libigl)


add_custom_target(my_custom_target
    COMMAND
        ${CMAKE_COMMAND} -E echo Hi this is a custom target ${GMP_LIBRARIES}
    VERBATIM
)

