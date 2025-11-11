cmake_minimum_required(VERSION 3.13)

# Set SDK path if not defined
if(NOT DEFINED PICO_SDK_PATH)
    set(PICO_SDK_PATH "${CMAKE_CURRENT_SOURCE_DIR}/lib/pico-sdk" CACHE PATH "Path to the Raspberry Pi Pico SDK")
    message(STATUS "PICO_SDK_PATH not set, defaulting to submodule: ${PICO_SDK_PATH}")
endif()

# Pull in SDK (must be before project)
include(pico_sdk_import.cmake)

# Set project name
project(pico_cmake_template_project C CXX ASM)

# Set C CXX standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialize the SDK
pico_sdk_init()

# Add application subdirectory
add_subdirectory(src)
