cmake_minimum_required(VERSION 3.0)

project(GameEdit)

# compile with static linking
set(CompilerFlags
        CMAKE_CXX_FLAGS
        CMAKE_CXX_FLAGS_DEBUG
        CMAKE_CXX_FLAGS_RELEASE
        CMAKE_CXX_FLAGS_MINSIZEREL
        CMAKE_CXX_FLAGS_RELWITHDEBINFO
        CMAKE_C_FLAGS
        CMAKE_C_FLAGS_DEBUG
        CMAKE_C_FLAGS_RELEASE
        CMAKE_C_FLAGS_MINSIZEREL
        CMAKE_C_FLAGS_RELWITHDEBINFO
        )
foreach(CompilerFlag ${CompilerFlags})
    string(REPLACE "/MD" "/MT" ${CompilerFlag} "${${CompilerFlag}}")
    set(${CompilerFlag} "${${CompilerFlag}}" CACHE STRING "msvc compiler flags" FORCE)
    message("MSVC flags: ${CompilerFlag}:${${CompilerFlag}}")
endforeach()

if (NOT TARGET imgui)
    add_subdirectory(imgui imgui)
endif ()

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

set(SOURCE_FILES "main.cpp" "imgui_impl_dx11.h" "imgui_impl_dx11.cpp" "imgui_impl_sdl.h" "imgui_impl_sdl.cpp")

add_executable(GameEdit WIN32 ${SOURCE_FILES})
target_link_libraries(GameEdit imgui)
target_link_libraries(GameEdit ${SDL2_LIBRARIES})
target_link_libraries(GameEdit d3d11.lib)

target_include_directories(GameEdit PUBLIC imgui)