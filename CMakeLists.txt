cmake_minimum_required(VERSION 3.15.0)
project(mario)

include(CTest)
enable_testing()

find_path(RAPIDXML_INCLUDE_PATH rapidxml/rapidxml.hpp)
find_path(IL_INCLUDE_PATH IL/il.h)
include_directories(${RAPIDXML_INCLUDE_PATH}/rapidxml)
include_directories(${IL_INCLUDE_PATH})

find_library(DEVIL_LIBRARY DevIL)

find_package(SDL2 REQUIRED)
find_package(SDL2-mixer REQUIRED)

include_directories(source)
add_subdirectory(source)
add_executable(mario Main.cpp)

target_link_libraries(mario
    SDL2::SDL2main
    SDL2::SDL2
    SDL2::SDL2_mixer
    ${DEVIL_LIBRARY}
    mario_lib
)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
