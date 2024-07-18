# Copyright (C) 2016-2023 by Sascha Willems - www.saschawillems.de
# This code is licensed under the MIT license (MIT) (http://opensource.org/licenses/MIT)

cmake_minimum_required(VERSION 3.4 FATAL_ERROR)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")

set(NAME dzVk)

project(${NAME})

include_directories(external)
include_directories(external/glm)
include_directories(external/imgui)
include_directories(external/tinygltf)
include_directories(external/ktx/include)
include_directories(external/ktx/other_include)
include_directories(base)

OPTION(USE_RELATIVE_ASSET_PATH "Load assets (shaders, models, textures) from a fixed path relative to the binar" OFF)
OPTION(FORCE_VALIDATION "Forces validation on for all samples at compile time (prefer using the -v / --validation command line arguments)" OFF)

set(RESOURCE_INSTALL_DIR "" CACHE PATH "Path to install resources to (leave empty for running uninstalled)")

# Use FindVulkan module added with CMAKE 3.7
message(STATUS "Using module to find Vulkan")
find_package(Vulkan)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DVK_USE_PLATFORM_WIN32_KHR")

IF (NOT Vulkan_FOUND)
	message(FATAL_ERROR "Could not find Vulkan library!")
ELSE()
	message(STATUS ${Vulkan_LIBRARY})
ENDIF()

# Set preprocessor defines
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DNOMINMAX -D_USE_MATH_DEFINES")

add_definitions(-D_CRT_SECURE_NO_WARNINGS)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB SOURCE *.cpp )

# Asset and shader path selection
if(RESOURCE_INSTALL_DIR)
	add_definitions(-DVK_EXAMPLE_ASSETS_DIR=\"${RESOURCE_INSTALL_DIR}/\")
	add_definitions(-DVK_EXAMPLE_SHADERS_DIR=\"${RESOURCE_INSTALL_DIR}/shaders/\")
	install(DIRECTORY assets/ DESTINATION ${RESOURCE_INSTALL_DIR}/)
	install(DIRECTORY shaders/ DESTINATION ${RESOURCE_INSTALL_DIR}/shaders/)
else()
	if(NOT USE_RELATIVE_ASSET_PATH)
		add_definitions(-DVK_EXAMPLE_ASSETS_DIR=\"${CMAKE_SOURCE_DIR}/assets/\")
		add_definitions(-DVK_EXAMPLE_SHADERS_DIR=\"${CMAKE_SOURCE_DIR}/shaders/\")
	endif()
endif()

# Force validation at compile time
if (FORCE_VALIDATION)
	add_definitions(-DFORCE_VALIDATION)
endif()

# Compiler specific stuff
IF(MSVC)
	SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")
ENDIF(MSVC)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/")

add_subdirectory(base)
add_subdirectory(examples)
