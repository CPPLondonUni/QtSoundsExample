cmake_minimum_required(VERSION 3.2)
project(QtSoundsExample)

set(CMAKE_CXX_STANDARD 14)

if (WIN32)
    message(NOTE "When building on Windows, You are expected to have QT installed to \\QT. Otherwise, you must set CMAKE_PREFIX_PATH manually")
    message(NOTE "Qt 5.10.1 is the default expected, please override this via QT_VERSION if you have a newer/older version of Qt5")
    set(QT_VERSION "5.10.1" CACHE PATH "Version of Qt5 you have installed")
    if (MSVC)
        message(NOTE "We currently only support MSVC2017. You will need to modify the CMakeLists.txt if you wish to use an older version.")
        set(CMAKE_PREFIX_PATH "C:\\Qt\\${QT_VERSION}\\msvc2017_64\\")
    else()
        set(CMAKE_PREFIX_PATH /Qt/${QT_VERSION}/mingw53_32/)
    endif()
    message(STATUS "Got Prefix path: ${CMAKE_PREFIX_PATH}")
endif()

find_package(Qt5 COMPONENTS Multimedia REQUIRED)

FILE(COPY Annoying_Alarm_Clock.wav DESTINATION ${CMAKE_BINARY_DIR})

add_executable(QtSoundsExample main.cpp)
target_link_libraries(QtSoundsExample Qt5::Multimedia)