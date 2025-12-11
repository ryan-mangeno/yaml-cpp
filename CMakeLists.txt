cmake_minimum_required(VERSION 3.16)
project(yaml-cpp CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB_RECURSE YAML_SOURCES "src/*.h" "src/*.cpp" "include/*.h")

add_library(yaml-cpp STATIC ${YAML_SOURCES})
target_include_directories(yaml-cpp PUBLIC "include")
target_compile_definitions(yaml-cpp PUBLIC YAML_CPP_STATIC_DEFINE)

if(UNIX OR APPLE)
    set_property(TARGET yaml-cpp PROPERTY POSITION_INDEPENDENT_CODE ON)
endif()