# ---------------------------------------------------
# CMakeLists.txt
#
# Author: Thomas Choquet <semoir.dense-0h@icloud.com>
# Date: 2024/10/07 09:43:21
# ---------------------------------------------------

cmake_minimum_required(VERSION 3.16)

set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build using shared libraries" FORCE)

option(TFD_BUILD_EXAMPLES "Build the example executable" OFF)
option(TFD_INSTALL        "Enable the install command"   ON)

project(tinyfiledialogs)
enable_language(C)

if(NOT CMAKE_RUNTIME_OUTPUT_DIRECTORY)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
endif()

if(NOT CMAKE_LIBRARY_OUTPUT_DIRECTORY)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
endif()

if(NOT CMAKE_ARCHIVE_OUTPUT_DIRECTORY)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
endif()

add_library(tinyfiledialogs)

file(GLOB_RECURSE TFD_SRC "src/*" "include/*")
target_sources(tinyfiledialogs PRIVATE ${TFD_SRC})

target_include_directories(tinyfiledialogs PRIVATE "src" PUBLIC "include")

if (TFD_BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()

if(UTILSCPP_INSTALL)
    install(TARGETS tinyfiledialogs
        RUNTIME DESTINATION "bin"
        LIBRARY DESTINATION "lib"
        ARCHIVE DESTINATION "lib"
    )
    install(DIRECTORY "include/" DESTINATION "include")
endif()