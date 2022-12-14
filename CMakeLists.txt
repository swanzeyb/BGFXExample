cmake_minimum_required(VERSION 3.0.0)
project(BGFXExample VERSION 0.1.0)

# Main executable
add_executable(BGFXExample main.cpp)

# Change these to your bgfx paths
set(BGFX_DIR ${PROJECT_SOURCE_DIR}/bgfx)

# Link static BGFX libraries
if (CMAKE_SYSTEM_NAME STREQUAL "Darwin")
  target_link_libraries(BGFXExample
    ${BGFX_DIR}/.build/osx-arm64/bin/libbxRelease.a
    ${BGFX_DIR}/.build/osx-arm64/bin/libbimgRelease.a
    ${BGFX_DIR}/.build/osx-arm64/bin/libbgfxRelease.a
  )
elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
  target_link_libraries(BGFXExample
    ${BGFX_DIR}/.build/win64_vs2022/bin/bxRelease.lib
    ${BGFX_DIR}/.build/win64_vs2022/bin/bimgRelease.lib
    ${BGFX_DIR}/.build/win64_vs2022/bin/bgfxRelease.lib
  )
endif()

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
