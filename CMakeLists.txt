cmake_minimum_required(VERSION 3.4)
# Set a project name.
project(main)
# Use the C++11 standard.
set(CMAKE_CXX_FLAGS "-std=c++11")
# Suppress warnings of the deprecation of glut functions on macOS.
if(APPLE)
  add_definitions(-Wno-deprecated-declarations)
endif()
# Find the packages we need.
find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLEW REQUIRED)
# Linux If not on macOS, we need glew.
if(UNIX AND NOT APPLE)
  find_package(GLEW REQUIRED)
endif()
set(INCLUDE_DIRS ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIR})
set(LIBRARIES ${OPENGL_LIBRARIES} ${GLUT_LIBRARIES})
if(UNIX AND NOT APPLE)
  list(APPEND INCLUDE_DIRS ${GLEW_INCLUDE_DIRS})
  list(APPEND LIBRARIES ${GLEW_LIBRARIES})
endif()
include_directories(${INCLUDE_DIRS})
file(GLOB SOURCE_FILES main.cpp src/*.cpp)
file(GLOB INCLUDE_FILES includes/*.h)
# Add the executable Example to be built from the source files.
add_executable(main ${SOURCE_FILES} ${INCLUDE_FILES})
# Link the executable to the libraries.
target_link_libraries(main ${LIBRARIES})
