cmake_minimum_required(VERSION 3.16.0 FATAL_ERROR)

################################################################################
# Set environment variables
################################################################################
set(ENV{PlatformTarget} ${CMAKE_VS_PLATFORM_NAME})
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ENV{PlatformArchitecture} "64")
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set(ENV{PlatformArchitecture} "86")
endif()

### imgui
FILE(GLOB ImGuiHeaderFiles *.h)
set(IMGUI_HEADER_FILES
        ${ImGuiHeaderFiles}
        "backends/imgui_impl_glfw.h"
        "backends/imgui_impl_opengl3.h"
        "backends/imgui_impl_opengl3_loader.h"
        "misc/cpp/imgui_stdlib.h"
)

FILE(GLOB ImGuiSourceFiles *.cpp)
set(IMGUI_SOURCE_FILES
        ${ImGuiSourceFiles}
        "backends/imgui_impl_glfw.cpp"
        "backends/imgui_impl_opengl3.cpp"
        "misc/cpp/imgui_stdlib.cpp"
)

add_library(imgui ${IMGUI_HEADER_FILES} ${IMGUI_SOURCE_FILES})

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    "${CMAKE_SOURCE_DIR}/includes/glfw-3.3.2.bin.WIN$ENV{PlatformArchitecture}/include;"
)
