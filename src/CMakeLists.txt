cmake_minimum_required(VERSION 2.8)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/../bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/../lib)


include_directories(.)

find_package(Boost 1.49.0 REQUIRED)
include_directories(${Boost_INCLUDE_DIRS})

add_executable(boost_example
    boost_example.cpp
)

add_executable(bitmap_test
    bitmap_test.cpp
    bitmap_image.hpp
)

# List your projects here to aid Visual Studio
set(PROJECTS
    bitmap_test
    boost_example
)

# This is to force visual studio to obey CMAKE_XXX_OUTPUT_DIRECTORY
# for this to work you need to list all you projects in a variable PROJECTS
if(MSVC)
    foreach(PROJECT ${PROJECTS})
        set_target_properties(${PROJECT} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})
        set_target_properties(${PROJECT} PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})
        foreach(OUTPUTCONFIG ${CMAKE_CONFIGURATION_TYPES})
            string(TOUPPER ${OUTPUTCONFIG} OUTPUTCONFIG)
            set_target_properties(${PROJECT} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})
            set_target_properties(${PROJECT} PROPERTIES LIBRARY_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})
        endforeach()
    endforeach()
endif()