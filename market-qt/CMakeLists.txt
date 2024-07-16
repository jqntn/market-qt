cmake_minimum_required(VERSION 3.15)

project(calculator LANGUAGES CXX)

set(QT_STATIC ON)
if (QT_STATIC)
    include(FetchContent)

    set(QT_VERSION_MAJOR 6)
    set(QT_VERSION_MINOR 7)
    set(QT_VERSION_PATCH 2)

    set(CMAKE_PROJECT_NAME "QtBase")
    set(CMAKE_AUTOMOC_EXECUTABLE "${CMAKE_BINARY_DIR}/bin/moc${CMAKE_EXECUTABLE_SUFFIX}")
    set(CMAKE_AUTOUIC_EXECUTABLE "${CMAKE_BINARY_DIR}/bin/uic${CMAKE_EXECUTABLE_SUFFIX}")

    set(FETCHCONTENT_QUIET OFF)

    FetchContent_Declare(qtbase URL https://github.com/qt/qtbase/archive/refs/tags/v${QT_VERSION_MAJOR}.${QT_VERSION_MINOR}.${QT_VERSION_PATCH}.tar.gz)
    FetchContent_MakeAvailable(qtbase)
else()
    find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets)
endif()

qt_standard_project_setup()

qt_add_executable(calculator
    main.cpp
    calculator.cpp
    button.cpp
)

set_target_properties(calculator PROPERTIES
    WIN32_EXECUTABLE TRUE
    MACOSX_BUNDLE TRUE
)

target_link_libraries(calculator PRIVATE
    Qt6::Core
    Qt6::Gui
    Qt6::Widgets
)