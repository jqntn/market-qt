cmake_minimum_required(VERSION 3.16)

project(market-qt LANGUAGES CXX)

if(QT_STATIC)
  set(QT_VERSION_MAJOR 6)
  set(QT_VERSION_MINOR 7)
  set(QT_VERSION_PATCH 2)

  set(FEATURE_optimize_size ON)
  set(FEATURE_static_runtime ON)

  set(BUILD_SHARED_LIBS OFF)

  set(CMAKE_PROJECT_NAME "QtBase")
  set(CMAKE_AUTOMOC_EXECUTABLE "${CMAKE_BINARY_DIR}/bin/moc${CMAKE_EXECUTABLE_SUFFIX}")
  set(CMAKE_AUTOUIC_EXECUTABLE "${CMAKE_BINARY_DIR}/bin/uic${CMAKE_EXECUTABLE_SUFFIX}")

  include(FetchContent)
  set(FETCHCONTENT_QUIET OFF)
  FetchContent_Declare(qtbase URL "https://github.com/qt/qtbase/archive/refs/tags/v${QT_VERSION_MAJOR}.${QT_VERSION_MINOR}.${QT_VERSION_PATCH}.tar.gz")
  FetchContent_MakeAvailable(qtbase)
else()
  find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets)
endif()

qt_standard_project_setup()

file(GLOB_RECURSE src "src/*.cpp" "include/*.h")
qt_add_executable(market-qt "${src}")

target_include_directories(market-qt PRIVATE
  "include")

target_link_libraries(market-qt PRIVATE
  Qt6::Core
  Qt6::Gui
  Qt6::Widgets)

if(QT_STATIC)
  target_link_libraries(market-qt PRIVATE
    "${CMAKE_BINARY_DIR}/plugins/platforms/qwindows.lib"
    imm32.lib
    d3d9.lib
    shcore.lib
    shlwapi.lib
    setupapi.lib
    wtsapi32.lib)

  target_compile_definitions(market-qt PRIVATE QT_STATIC)
endif()

set_target_properties(market-qt PROPERTIES
  WIN32_EXECUTABLE ON
  MACOSX_BUNDLE ON)