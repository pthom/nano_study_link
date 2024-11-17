cmake_minimum_required(VERSION 3.19)
project(nano_study_link LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

# Add imgui (a custom version, from imgui bundle, very close to the original)
add_library(imgui STATIC
    imgui/imgui.cpp imgui/imgui_draw.cpp imgui/imgui_widgets.cpp imgui/imgui_demo.cpp imgui/imgui_tables.cpp
    imgui/imgui_stacklayout.cpp
)
target_compile_definitions(imgui PUBLIC IMGUI_BUNDLE_PYTHON_API)
target_include_directories(imgui PUBLIC imgui)


# From https://nanobind.readthedocs.io/en/latest/building.html
macro(setup_nanobind)
    if (CMAKE_VERSION VERSION_LESS 3.18)
        set(DEV_MODULE Development)
    else()
        set(DEV_MODULE Development.Module)
    endif()
    find_package(Python 3.8 COMPONENTS Interpreter ${DEV_MODULE} REQUIRED)

    if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
        set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build." FORCE)
        set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
    endif()
    add_subdirectory(nanobind)
endmacro()

# Build nanobind bindings
setup_nanobind()
nanobind_add_module(nanobind_imgui nanobind_imgui.cpp)
target_link_libraries(nanobind_imgui PRIVATE imgui)

