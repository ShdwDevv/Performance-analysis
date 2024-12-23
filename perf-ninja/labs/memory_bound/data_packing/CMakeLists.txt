cmake_minimum_required(VERSION 3.3)

project(lab)

# Detect the compiler and set flags accordingly
if(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    # Clang-specific flags
    set(CMAKE_CXX_FLAGS "-mllvm -align-all-functions=6 ${CMAKE_CXX_FLAGS}")
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    # GCC-specific flags, replace -align-all-functions=6 with -falign-functions
    set(CMAKE_CXX_FLAGS "-falign-functions=6 ${CMAKE_CXX_FLAGS}")
else()
    message(WARNING "Unknown compiler, please check flag compatibility.")
endif()

# Mitigate the impact of code alignment (for GCC, Clang, or other compilers)
# Make sure to add compiler-specific flags based on what the system supports.

# Regular expressions to match and extract repo path
string(REGEX MATCH "^(.*)[\\/]labs[\\/].*$" repo "${CMAKE_CURRENT_SOURCE_DIR}")
include(${CMAKE_MATCH_1}/tools/labs.cmake)