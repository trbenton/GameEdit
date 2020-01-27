cmake_minimum_required(VERSION 3.0)

project(imgui)

set(SOURCE_FILES "imconfig.h" "imgui.h" "imgui.cpp" "imgui_demo.cpp" "imgui_draw.cpp" "imgui_internal.h"
                 "imgui_widgets.cpp" "imstb_rectpack.h" "imstb_textedit.h" "imstb_truetype.h")

add_library(imgui STATIC ${SOURCE_FILES})