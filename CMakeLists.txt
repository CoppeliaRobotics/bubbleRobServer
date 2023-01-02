cmake_minimum_required(VERSION 3.15)
project(bubbleRobServer)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_MACOSX_RPATH 1)

find_package(Boost REQUIRED COMPONENTS system)

if(NOT LIBPLUGIN_DIR)
    if(DEFINED ENV{COPPELIASIM_ROOT_DIR})
        set(LIBPLUGIN_DIR $ENV{COPPELIASIM_ROOT_DIR}/programming/libPlugin)
    else()
        set(LIBPLUGIN_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../libPlugin)
    endif()
endif()
list(APPEND CMAKE_MODULE_PATH ${LIBPLUGIN_DIR}/cmake)
find_package(CoppeliaSim 4.5.0.0 REQUIRED)

coppeliasim_add_executable(bubbleRobServer
    SOURCES
    bubbleRobServer.cpp
    ${COPPELIASIM_COMMON_DIR}/socketInConnection.cpp
)
target_include_directories(bubbleRobServer PRIVATE ${COPPELIASIM_INCLUDE_DIR})
target_link_libraries(bubbleRobServer Boost::system)
