cmake_minimum_required(VERSION 3.4)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "Choose the type of build (Debug or Release)")
endif()

project(pong)
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake_modules" ${CMAKE_MODULE_PATH})
set(SFML_STATIC_LIBRARIES ON CACHE BOOL "Utilitza llibreries estàtiques")
set(SFML_ROOT "" CACHE PATH "Lloc on s'ha instal·lat SFML")
find_package(SFML 2 REQUIRED system window graphics audio)
include_directories(${SFML_INCLUDE_DIR})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(DEV_BUILD OFF CACHE BOOL "Si s'ha de compilar per a desenvolupadors (vides infinites)")
if (DEV_BUILD)
    add_definitions("-DDEV_BUILD=1")
else ()
    add_definitions("-DDEV_BUILD=0")
endif ()

add_executable(pong main.cpp Pala.cpp Pilota.cpp Marcador.cpp Title.cpp)
target_link_libraries(pong ${SFML_LIBRARIES} ${SFML_DEPENDENCIES}
    ${SFML_system_DEPENDENCIES} ${SFML_window_DEPENDENCIES}
    ${SFML_graphics_DEPENDENCIES} ${SFML_audio_DEPENDENCIES})

file(COPY "${CMAKE_SOURCE_DIR}/assets" DESTINATION "${CMAKE_BINARY_DIR}")