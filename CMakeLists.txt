cmake_minimum_required(VERSION 3.16)
project(yaml-cpp CXX)

# ==========================================
# Standard Setup (C++17)
# ==========================================
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# ==========================================
# Sources
# ==========================================
# Replicating Premake's "src/**.cpp" recursive search
file(GLOB_RECURSE YAML_SOURCES 
    "src/*.h"
    "src/*.cpp"
    "include/*.h"
)

# ==========================================
# Define Target
# ==========================================
add_library(yaml-cpp STATIC ${YAML_SOURCES})

# ==========================================
# Includes & Defines
# ==========================================
# Expose "include" folder to projects linking this lib
target_include_directories(yaml-cpp PUBLIC "include")

# Define macro for static build
target_compile_definitions(yaml-cpp PUBLIC YAML_CPP_STATIC_DEFINE)

# ==========================================
# Platform Specifics
# ==========================================
# Linux: "pic On" -> Position Independent Code
if(UNIX AND NOT APPLE)
    set_property(TARGET yaml-cpp PROPERTY POSITION_INDEPENDENT_CODE ON)
endif()

# Windows: "staticruntime off"
# This is the CMake default, so no special "MSVC_RUNTIME_LIBRARY" flags are needed.