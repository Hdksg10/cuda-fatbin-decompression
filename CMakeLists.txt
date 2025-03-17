cmake_minimum_required(VERSION 3.18 FATAL_ERROR)
project(cuda-fatbin-decompression)

set(CMAKE_C_STANDARD 11)

set(SRC_FILES fatbin-decompress.c utils.c main.c)

add_executable(cuda-fatbin-decompress ${SRC_FILES})
add_library(fatbin-decompress SHARED ${SRC_FILES})
target_include_directories(cuda-fatbin-decompress PRIVATE ${CMAKE_SOURCE_DIR})
target_include_directories(fatbin-decompress PRIVATE ${CMAKE_SOURCE_DIR})

# Add debug flags if needed
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_options(cuda-fatbin-decompress PRIVATE -g)
    target_compile_options(fatbin-decompress PRIVATE -g)
endif()