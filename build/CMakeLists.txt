cmake_minimum_required(VERSION 3.10)
project(mipgen_standalone)

get_filename_component(DIR_ONE_ABOVE ../ ABSOLUTE)
include(ExternalProject)

ExternalProject_Add(
    robin-map
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/robin-map/tnt
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/robin-map/tnt
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/robin-map/tnt
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    libz
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/libz
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/libz
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/libz
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    astcenc 
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/astcenc/tnt
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/astcenc/tnt
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/astcenc/tnt
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    etc2comp 
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/etc2comp/
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/etc2comp/
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/etc2comp
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    stb 
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/stb/tnt
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/stb/tnt
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/stb/tnt
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    tinyexr
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/tinyexr/tnt
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/tinyexr/tnt
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/tinyexr/tnt
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    getopt
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/getopt
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/getopt
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/getopt
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    libpng
    SOURCE_DIR ${DIR_ONE_ABOVE}/third_party/libpng/tnt
    BINARY_DIR ${DIR_ONE_ABOVE}/third_party/libpng/tnt
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/third_party/libpng/tnt
    INSTALL_COMMAND ""
)

ExternalProject_Add(
    math
    SOURCE_DIR ${DIR_ONE_ABOVE}/libs/math
    BINARY_DIR ${DIR_ONE_ABOVE}/libs/math
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/libs/math
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    utils 
    SOURCE_DIR ${DIR_ONE_ABOVE}/libs/utils
    BINARY_DIR ${DIR_ONE_ABOVE}/libs/utils
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/libs/utils
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    image 
    SOURCE_DIR ${DIR_ONE_ABOVE}/libs/image
    BINARY_DIR ${DIR_ONE_ABOVE}/libs/image
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/libs/image
    INSTALL_COMMAND ""
)
ExternalProject_Add(
    imageio 
    SOURCE_DIR ${DIR_ONE_ABOVE}/libs/imageio
    BINARY_DIR ${DIR_ONE_ABOVE}/libs/imageio
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/libs/imageio
    INSTALL_COMMAND ""
)

ExternalProject_Add(
    mipgen 
    SOURCE_DIR ${DIR_ONE_ABOVE}/tool
    BINARY_DIR ${DIR_ONE_ABOVE}/tool
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${DIR_ONE_ABOVE}/tool
    INSTALL_COMMAND ""
)

add_dependencies(utils robin-map)
add_dependencies(image utils)
add_dependencies(imageio astcenc)
add_dependencies(imageio etc2comp)
add_dependencies(imageio stb)
add_dependencies(imageio tinyexr)
add_dependencies(imageio image)
add_dependencies(imageio getopt)
add_dependencies(imageio libpng)
add_dependencies(mipgen imageio)
