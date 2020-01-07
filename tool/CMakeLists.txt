cmake_minimum_required(VERSION 3.10)
project(mipgen)

set(TARGET mipgen)

get_filename_component(DIR_ONE_ABOVE ../ ABSOLUTE)

find_package(Threads)

link_directories(
    ${DIR_ONE_ABOVE}/libs/math 
    ${DIR_ONE_ABOVE}/libs/utils
    ${DIR_ONE_ABOVE}/libs/image
    ${DIR_ONE_ABOVE}/libs/imageio
    ${DIR_ONE_ABOVE}/third_party/getopt
    ${DIR_ONE_ABOVE}/third_party/libpng/tnt
    ${DIR_ONE_ABOVE}/third_party/etc2comp/EtcLib
    ${DIR_ONE_ABOVE}/third_party/libz
    ${DIR_ONE_ABOVE}/third_party/stb
    ${DIR_ONE_ABOVE}/third_party/tinyexr/tnt
    ${DIR_ONE_ABOVE}/third_party/astcenc/tnt
)

# ==================================================================================================
# Source files
# ==================================================================================================
set(SRCS src/main.cpp)

# ==================================================================================================
# Target definitions
# ==================================================================================================
add_executable(${TARGET} ${SRCS})
target_link_libraries(${TARGET} PRIVATE math utils z image imageio getopt png tinyexr astcenc EtcLib ${CMAKE_THREAD_LIBS_INIT})

# =================================================================================================
# Licenses
# ==================================================================================================
#set(MODULE_LICENSES getopt libpng tinyexr libz astcenc stb etc2comp)
#set(GENERATION_ROOT ${CMAKE_CURRENT_BINARY_DIR}/generated)
#list_licenses(${GENERATION_ROOT}/licenses/licenses.inc ${MODULE_LICENSES})
#target_include_directories(${TARGET} PRIVATE ${GENERATION_ROOT})

# ==================================================================================================
# Installation
# ==================================================================================================
#install(TARGETS ${TARGET} RUNTIME DESTINATION bin)
#install(FILES "README.md" DESTINATION docs/ RENAME "${TARGET}.md")
