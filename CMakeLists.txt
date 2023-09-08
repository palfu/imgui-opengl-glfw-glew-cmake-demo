cmake_minimum_required(VERSION 3.6)
project(imgui-demo)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_VERBOSE_MAKEFILE 1)
set(APP_VERSION_MAJOR 1)
set(APP_VERSION_MINOR 0)

set(APP_TARGET app)

file(GLOB_RECURSE IMGUI_SRCS
    imgui/*.cpp
)

include_directories(imgui)

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
