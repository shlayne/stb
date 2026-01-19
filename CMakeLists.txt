cmake_minimum_required(VERSION 4.2)

project(stb)

if(MSVC) # TODO: non-msvc
    set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_SOLUTION_ITEMS
        .gitattributes
        .gitignore
        .travis.yml
        CMakeLists.txt
        LICENSE
        README.md
        SECURITY.md
    )
endif()

add_library(stb INTERFACE)
file(GLOB_RECURSE PROJECT_SOURCES CONFIGURE_DEPENDS
    ${CMAKE_CURRENT_SOURCE_DIR}/stb_*.h
)
target_sources(stb PRIVATE ${PROJECT_SOURCES})
target_include_directories(stb INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})

if(NOT "${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_CURRENT_SOURCE_DIR}")
    set_target_properties(stb PROPERTIES FOLDER Dependencies)
endif()
