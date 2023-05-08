cmake_minimum_required(VERSION 3.5)

project(ide4pplc VERSION 0.1 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets REQUIRED)

add_subdirectory(lib)

set(SOURCE_FILES
    src/main.cpp
    src/mainwindow.cpp
)

set(INCLUDE_FILES
    include/mainwindow.h
)

set(FORM_FILES
    forms/mainwindow.ui
)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(ide4pplc
        MANUAL_FINALIZATION
        ${SOURCE_FILES}
        ${INCLUDE_FILES}
        ${FORM_FILES}
    )
else()
    add_executable(ide4pplc
        ${SOURCE_FILES}
        ${INCLUDE_FILES}
        ${FORM_FILES}
    )
endif()

target_include_directories(ide4pplc PUBLIC
    include
)

target_link_libraries(ide4pplc PRIVATE Qt${QT_VERSION_MAJOR}::Widgets QCodeEditor)

set_target_properties(ide4pplc PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
)


if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(ide4pplc)
endif()
