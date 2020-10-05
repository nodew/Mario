cmake_minimum_required(VERSION 3.15.0)
project(mario_lib)

find_path(RAPIDXML_INCLUDE_PATH rapidxml/rapidxml.hpp)
find_path(IL_INCLUDE_PATH IL/il.h)
include_directories(${RAPIDXML_INCLUDE_PATH}/rapidxml)
include_directories(${IL_INCLUDE_PATH})

find_library(DEVIL_LIBRARY DevIL)

find_package(OpenGL REQUIRED)
find_package(SDL2 REQUIRED)
find_package(SDL2-mixer REQUIRED)

aux_source_directory(. MARIO_LIB_FILES)
file(GLOB LEVEL_GENERATORS "LevelGenerators/*")

add_library(mario_lib ${MARIO_LIB_FILES} ${LEVEL_GENERATORS})

target_link_libraries(mario_lib
    ${OPENGL_LIBRARIES}
    ${DEVIL_LIBRARY}
    SDL2::SDL2main
    SDL2::SDL2
    SDL2::SDL2_mixer
)

