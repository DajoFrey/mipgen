cmake_minimum_required(VERSION 3.10)
project(imageio)

set(TARGET imageio)
set(PUBLIC_HDR_DIR include)

get_filename_component(DIR_ONE_ABOVE ../ ABSOLUTE)
get_filename_component(DIR_TWO_ABOVE ../../ ABSOLUTE)

# ==================================================================================================
# Sources and headers
# ==================================================================================================
#set(PUBLIC_HDRS
#        include/imageio/BlockCompression.h
#        include/imageio/ImageDecoder.h
#        include/imageio/ImageDiffer.h
#        include/imageio/ImageEncoder.h
#)

set(SRCS
        src/BlockCompression.cpp
        src/ImageDecoder.cpp
        src/ImageDiffer.cpp
        src/ImageEncoder.cpp
)

# ==================================================================================================
# Include and target definitions
# ==================================================================================================
include_directories(${PUBLIC_HDR_DIR})

add_library(${TARGET} STATIC ${PUBLIC_HDRS} ${SRCS})

target_include_directories(${TARGET} PUBLIC ${PUBLIC_HDR_DIR})

link_directories(
    ${DIR_ONE_ABOVE}/utils
    ${DIR_ONE_ABOVE}/image
    ${DIR_ONE_ABOVE}/math
    ${DIR_TWO_ABOVE}/third_party/libpng/tnt
    ${DIR_TWO_ABOVE}/third_party/tinyexr/tnt
    ${DIR_TWO_ABOVE}/third_party/libz
    ${DIR_TWO_ABOVE}/third_party/astcenc/tnt
    ${DIR_TWO_ABOVE}/third_party/stb/tnt
    ${DIR_TWO_ABOVE}/third_party/etc2comp/EtcLib
)

target_link_libraries(${TARGET} PUBLIC image math png tinyexr utils z astcenc stb EtcLib)
if (WIN32)
    target_link_libraries(${TARGET} PRIVATE wsock32)
endif()

# ==================================================================================================
# Compiler flags
# ==================================================================================================
if (NOT MSVC_NATIVE)
    target_compile_options(${TARGET} PRIVATE -Wno-deprecated-register)
endif()

if (MSVC OR CLANG_CL)
    target_compile_options(${TARGET} PRIVATE $<$<CONFIG:Release>:/fp:fast>)
else()
    target_compile_options(${TARGET} PRIVATE $<$<CONFIG:Release>:-ffast-math>)
endif()
