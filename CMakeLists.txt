cmake_minimum_required(VERSION 3.0.0)
project(BGFXExample VERSION 0.1.0)
set(CMAKE_CXX_STANDARD 11)

# Includes
include(FetchContent)

# Source files
set(SOURCE_FILES
  main.cpp
)

# Change this to your bgfx path
set(BGFX_DIR ${PROJECT_SOURCE_DIR}/external/bgfx)

# Add CrossWindow library
add_subdirectory(external/crosswindow)
xwin_add_executable(${PROJECT_NAME}
  "${SOURCE_FILES}"
)
target_link_libraries(
    ${PROJECT_NAME}
    CrossWindow
)

# Link static BGFX libraries
if (CMAKE_SYSTEM_NAME STREQUAL "Darwin")
  set(CMAKE_CXX_FLAGS "-ObjC++")
  target_link_libraries(${PROJECT_NAME}
    "-framework ServiceManagement"
    "-framework Foundation"
    "-framework Cocoa"
    "-framework Metal"
    "-framework IOKit"
    "-framework QuartzCore"
    ${BGFX_DIR}/.build/osx-arm64/bin/libbxRelease.a
    ${BGFX_DIR}/.build/osx-arm64/bin/libbimgRelease.a
    ${BGFX_DIR}/.build/osx-arm64/bin/libbgfxRelease.a
  )
elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
  target_link_libraries(${PROJECT_NAME}
    ${BGFX_DIR}/.build/win64_vs2022/bin/bxRelease.lib
    ${BGFX_DIR}/.build/win64_vs2022/bin/bimgRelease.lib
    ${BGFX_DIR}/.build/win64_vs2022/bin/bgfxRelease.lib
  )
endif()

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
