cmake_minimum_required(VERSION 3.0.0)
project(BGFXExample VERSION 0.1.0)

include(CTest)
enable_testing()

add_executable(BGFXExample main.cpp)

target_link_libraries(BGFXExample
  ${PROJECT_SOURCE_DIR}/bgfx/.build/osx-arm64/bin/libbxRelease.a
  ${PROJECT_SOURCE_DIR}/bgfx/.build/osx-arm64/bin/libbimgRelease.a
  ${PROJECT_SOURCE_DIR}/bgfx/.build/osx-arm64/bin/libbgfxRelease.a
)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
