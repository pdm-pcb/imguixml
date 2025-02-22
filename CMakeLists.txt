cmake_minimum_required(VERSION 3.25) # Required for FetchContent SYSTEM

project(
    imguixml
    VERSION 0.1.0
    DESCRIPTION ""
    LANGUAGES CXX C
)

find_package(Vulkan 1.3 REQUIRED)

list(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake")

include("set_target_arch")
include("add_debug_flags")
include("add_release_flags")

set_target_arch()
add_debug_flags()
add_release_flags()

add_subdirectory(imgui)

include("fetch_glfw3")
fetch_glfw3()

set(CMAKE_CXX_STANDARD          23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS        OFF)

set(CMAKE_C_STANDARD            23)
set(CMAKE_C_STANDARD_REQUIRED   ON)
set(CMAKE_C_EXTENSIONS          OFF)

include("add_compiler_definitions")
include("add_warning_flags")

add_compiler_definitions()
add_warning_flags()

add_executable(${PROJECT_NAME})

target_sources(${PROJECT_NAME} PRIVATE "main.cpp")

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR})

target_link_libraries(${PROJECT_NAME}
PRIVATE
    Vulkan::Vulkan
    glfw
    imgui
)