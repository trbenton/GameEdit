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

set(SOURCE_FILES "main.cpp" "imgui_impl_dx12.h" "imgui_impl_dx12.cpp" "imgui_impl_win32.h" "imgui_impl_win32.cpp")

add_executable(GameEdit WIN32 ${SOURCE_FILES})
target_link_libraries(GameEdit imgui)
target_link_libraries(GameEdit d3d12.lib)
target_link_libraries(GameEdit dxgi.lib)

target_include_directories(GameEdit PUBLIC imgui)