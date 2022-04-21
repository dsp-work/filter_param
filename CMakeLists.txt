cmake_minimum_required(VERSION 3.16)

# project name
project(digital_filters CXX)

#--------------- CMake compile config ------------------------------
include(./.cmake/cxx_config.cmake)

#----------------- clang-format config -------------------------
include(./.cmake/clang-format.cmake)


#------------------ build source config ------------------

# include path
include_directories(include)

# sub directory
add_subdirectory(lib)

# libraries
add_library(digital_filters INTERFACE)
    target_link_libraries(digital_filters INTERFACE cascade_iir)

# for development executable(optional activate)
option(DEVELOP_EXECUTABLE_DIGITAL_FILTERS "Build develop executable file on digital filters package" OFF)
if(DEVELOP_EXECUTABLE_DIGITAL_FILTERS)
# executables
    add_executable(develop_main develop_main.cpp)
    target_link_libraries(develop_main digital_filters)
endif()

# for tests
if(NOT without-test)
    enable_testing()
    add_subdirectory(test)
endif()
