cmake_minimum_required(VERSION 3.6)
project(imgui-demo)

set(CMAKE_CXX_FLAGS "$ENV{CXXFLAGS} -std=c++14 -O3 -g -Wall -fPIC -fopenmp -pthread")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -std=c++14 -O3 -Wall -fPIC -fopenmp -pthread")

# set(CMAKE_CXX_STANDARD 11)
set(CMAKE_VERBOSE_MAKEFILE 1)
set(APP_VERSION_MAJOR 1)
set(APP_VERSION_MINOR 0)

set(APP_TARGET app)

message("CMAKE_CURRENT_SOURCE_DIR: ${CMAKE_CURRENT_SOURCE_DIR}")

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/src/imgui
    ${CMAKE_CURRENT_SOURCE_DIR}/src/implot
    ${CMAKE_CURRENT_SOURCE_DIR}/src/zmo)

file(GLOB_RECURSE IMGUI_SRCS
    src/imgui/*.cpp
    src/implot/*.cpp
    src/imnodes/*.cpp
    src/imGuiFileDialog/*.cpp
    src/zmo/*.cpp
    src/imCoolBar/*.cpp
    src/imspinner/*.cpp
    src/node_editor/*.cpp
)

find_package(glfw3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})
link_libraries(${GLFW_LIBRARY_DIRS})

find_package(OpenGL REQUIRED)

# include_directories(${OPENGL_INCLUDE_DIRS})

# find_package(GLEW REQUIRED)
# include_directories(${GLEW_INCLUDE_DIRS})
add_library(imgui SHARED ${IMGUI_SRCS})
target_link_libraries(imgui glfw ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES})

add_executable(${APP_TARGET} main.cpp)
target_link_libraries(${APP_TARGET} imgui)

add_executable(zmo zmo_main.cpp)
target_link_libraries(zmo imgui)