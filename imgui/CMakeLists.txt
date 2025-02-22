add_library(imgui STATIC)

file(GLOB sources "*.cpp")
file(GLOB headers "*.h")

target_sources(imgui PRIVATE ${sources} PRIVATE ${headers})

target_include_directories(imgui PUBLIC ${CMAKE_SOURCE_DIR})

target_link_libraries(imgui
PUBLIC
    Vulkan::Vulkan
    glfw
)