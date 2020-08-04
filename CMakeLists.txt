project(PolyTrix)

cmake_minimum_required(VERSION 3.0)

set(OUTPUT_DIR ${CMAKE_HOME_DIRECTORY}/target/)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_DIR})
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${OUTPUT_DIR})
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${OUTPUT_DIR})
SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${OUTPUT_DIR})
SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${OUTPUT_DIR})
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${OUTPUT_DIR})
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${OUTPUT_DIR})

set(src src/PolyTrix.cpp src/MatrixAccountSession.cpp)
include_directories(src)

# Support for better async stuff with futures using thousandeyes-futures.
add_subdirectory("thousandeyes-futures")
include_directories("thousandeyes-futures/include")

# Use libmatrix-client
SET(USE_CONAN OFF CACHE BOOL "Don't use conan in libmatrix-client")
SET(USE_CPPRESTSDK OFF CACHE BOOL "Don't use CPPRESTSDK (directly) in libmatrix-client")


# Use our interface with PolyChat's supplied HTTP sessions
add_compile_definitions("USE_CUSTOM_HTTP_SESSION")

add_subdirectory("libmatrix-client")
include_directories("libmatrix-client/include")


# define the project
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include("${CMAKE_CURRENT_SOURCE_DIR}/static.cmake")
include("${CMAKE_CURRENT_SOURCE_DIR}/shared.cmake")