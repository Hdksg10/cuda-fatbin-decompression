cmake_minimum_required(VERSION 3.18 FATAL_ERROR)
project(cuda_fatbin_decompression)
option(FATBIN_DECOMPRESS_DEBUG "Enable debug output" OFF)
set(CMAKE_C_STANDARD 11)

set(SRC_FILES fatbin-decompress.c utils.c)

add_library(fatbin SHARED fatbin-decompress.c utils.c)
target_include_directories(fatbin PRIVATE ${CMAKE_SOURCE_DIR})

add_executable(cuda_fatbin_decompress main.c)
target_include_directories(cuda_fatbin_decompress PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(cuda_fatbin_decompress PRIVATE fatbin)

# Add debug flags if needed
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_options(cuda_fatbin_decompress PRIVATE -g)
    target_compile_options(fatbin PRIVATE -g)
endif()

if(FATBIN_DECOMPRESS_DEBUG)
    target_compile_definitions(cuda_fatbin_decompress PRIVATE FATBIN_DECOMPRESS_DEBUG)
    target_compile_definitions(fatbin PRIVATE FATBIN_DECOMPRESS_DEBUG)
endif()