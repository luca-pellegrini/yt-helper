cmake_minimum_required(VERSION 3.5)

project(yt-helper VERSION 0.1 LANGUAGES CXX)

## Defines ##

# Create main application target
set(YT_HELPER_TARGET "yt-helper")

## Defines end ##

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets)

set(PROJECT_SOURCES
    src/main.cpp
    src/mainwindow.h
    src/mainwindow.cpp
)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(${YT_HELPER_TARGET}
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
    )
    # For more information, see https://doc.qt.io/qt-6/qt-add-executable.html#target-creation
else()
    add_executable(${YT_HELPER_TARGET}
        ${PROJECT_SOURCES}
    )
endif()

# Set link libraries
target_link_libraries(${YT_HELPER_TARGET}
    PRIVATE
    Qt${QT_VERSION_MAJOR}::Widgets
)

## Install ##

# Copy executable
install(TARGETS ${YT_HELPER_TARGET})

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(${YT_HELPER_TARGET})
endif()

## Install end ##
