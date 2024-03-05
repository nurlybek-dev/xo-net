cmake_minimum_required(VERSION 3.20)
project(xo VERSION 0.1.0 LANGUAGES C CXX)

include(CTest)
enable_testing()

find_package(PkgConfig REQUIRED)
pkg_search_module(SDL2 REQUIRED sdl2)
find_package(SDL2 REQUIRED)
# pkg_search_module(SDL2_image REQUIRED)
# pkg_search_module(SDL2_ttf REQUIRED)
# pkg_search_module(SDL2_net REQUIRED)
# pkg_search_module(SDL2_gfx REQUIRED)
# pkg_search_module(SDL2_mixer REQUIRED)

include_directories(imgui)
include_directories(imgui/backends)

set(IMGUI_DIR "imgui")

file(GLOB_RECURSE PLANES_SRC CONFIGURE_DEPENDS "src/*.h" "src/*.cpp")

add_executable(
    xo 
    main.cpp
    ${PLANES_SRC} 
    ${IMGUI_DIR}/imgui.cpp ${IMGUI_DIR}/imgui_demo.cpp ${IMGUI_DIR}/imgui_draw.cpp ${IMGUI_DIR}/imgui_tables.cpp ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/backends/imgui_impl_sdl2.cpp ${IMGUI_DIR}/backends/imgui_impl_sdlrenderer2.cpp
)

target_include_directories(xo PRIVATE ${SDL2_INCLUDE_DIRS})
target_link_libraries(xo ${SDL2_LIBRARIES} ${SDL2_IMAGE_LIBRARIES} ${SDL2_TTF_LIBRARIES})

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
