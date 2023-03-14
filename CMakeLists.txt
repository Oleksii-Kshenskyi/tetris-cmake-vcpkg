cmake_minimum_required(VERSION 3.26)

set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
  CACHE STRING "Vcpkg toolchain file")
project(tetris-sfml-cmake)

set(SRC_DIR src)

set(SFML_STATIC_LIBRARIES TRUE)
find_package(SFML COMPONENTS window graphics system)
include_directories(${SRC_DIR})
add_executable(tetris ${SRC_DIR}/main.cpp)
target_link_libraries(tetris sfml-graphics)
set_target_properties(tetris PROPERTIES CXX_STANDARD 20
                                        CXX_STANDARD_REQUIRED ON)

add_custom_command(TARGET tetris POST_BUILD
COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/images ${CMAKE_BINARY_DIR}/images)