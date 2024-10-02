cmake_minimum_required(VERSION 3.16)
project(mygame)

# https://cmake.org/cmake/help/latest/prop_tgt/CXX_STANDARD.html
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Fetch raylib hvis det ikke allerede er i build-mappen
include(FetchContent)

set(RAYLIB_VERSION 5.0)
FetchContent_Declare(
    raylib
    URL https://github.com/raysan5/raylib/archive/refs/tags/${RAYLIB_VERSION}.tar.gz
    FIND_PACKAGE_ARGS ${RAYLIB_VERSION}
)
set(BUILD_EXAMPLES OFF CACHE INTERNAL "")
FetchContent_MakeAvailable(raylib)

# Kan brukes for å hente hele raygui hvis man trenger flere filer
# SKAL samsvare med raylib - dvs. nyeste versjon med nyeste versjon
#[[
set(RAYGUI_VERSION 4.0)
FetchContent_Declare(
    raygui
    URL https://github.com/raysan5/raygui/archive/refs/tags/${RAYGUI_VERSION}.tar.gz
	FIND_PACKAGE_ARGS ${RAYGUI_VERSION}
)
set(BUILD_EXAMPLES OFF CACHE INTERNAL "")
FetchContent_MakeAvailable(raygui) #samle raylib og raygui til en fil om det fungerer
]]

#Include dir
include_directories(
	"${PROJECT_SOURCE_DIR}/include"
	"${PROJECT_SOURCE_DIR}/include/Audio"
    "${PROJECT_SOURCE_DIR}/include/Entities"
    "${PROJECT_SOURCE_DIR}/include/GUI"
    "${PROJECT_SOURCE_DIR}/include/Level"
    "${PROJECT_SOURCE_DIR}/include/Menu"
	"${PROJECT_SOURCE_DIR}/assets/raygui"    
)
# src dir
include_directories(
	"${PROJECT_SOURCE_DIR}/src"
    "${PROJECT_SOURCE_DIR}/src/Audio"   
    "${PROJECT_SOURCE_DIR}/src/Entities" 
    "${PROJECT_SOURCE_DIR}/src/GUI" 
    "${PROJECT_SOURCE_DIR}/src/Level" 
    "${PROJECT_SOURCE_DIR}/src/Menu" 
)
# raygui subdir
add_subdirectory(assets/raygui)

#alle src filer
file(GLOB all_SRCS
	"${PROJECT_SOURCE_DIR}/src/*.h"
    "${PROJECT_SOURCE_DIR}/src/*.cpp"
    "${PROJECT_SOURCE_DIR}/src/Audio/*.cpp"   
    "${PROJECT_SOURCE_DIR}/src/Entities/*.cpp" 
    "${PROJECT_SOURCE_DIR}/src/GUI/*.cpp" 
    "${PROJECT_SOURCE_DIR}/src/Level/*.cpp" 
    "${PROJECT_SOURCE_DIR}/src/Menu/*.cpp"
)

# .exe fil fra alle src-filer
add_executable(${PROJECT_NAME} ${all_SRCS})

# This is useful to get an ASSETS_PATH in your IDE during development
target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC RESOURCES_PATH="${PROJECT_SOURCE_DIR}/assets/")
target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC PRODUCTION_BUILD=0) 

# debug settings
#target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC _CRT_SECURE_NO_WARNINGS)
#set_target_properties("${CMAKE_PROJECT_NAME}" PROPERTIES LINK_FLAGS "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup") #no console

# Link and include raylib
target_link_libraries(${PROJECT_NAME} raylib)