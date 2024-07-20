cmake_minimum_required(VERSION 3.10)

# Descriptions for the project
set(PROJ_NAME cmaker)
set(VER 0.0.1)
set(CPP_STD 17)

project(${PROJ_NAME} VERSION ${VER} LANGUAGES C CXX)

string(COMPARE EQUAL ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_SOURCE_DIR} PROJECT_IS_IN_ROOT)
set(CMAKE_EXPORT_COMPILE_COMMANDS ${PROJECT_IS_IN_ROOT})

if(PROJECT_IS_IN_ROOT)
    set(CMAKE_CXX_STANDARD ${CPP_STD})
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    message(STATUS "Project ${PROJECT_NAME}:${VER} is in root.")
endif(PROJECT_IS_IN_ROOT)

option(HAS_TESTS "Build and perform tests" ${PROJECT_IS_IN_ROOT})
option(HAS_BENCHES "Build and perform benches" ${PROJECT_IS_IN_ROOT})
option(HAS_EXAMPLES "Build and perform examples" ${PROJECT_IS_IN_ROOT})

# Includes
set(SRC_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/src/include)
include_directories(${SRC_INCLUDE_DIR})

add_subdirectory(${PROJECT_SOURCE_DIR}/src)

if(PROJECT_IS_IN_ROOT)
    include(${CMAKE_SOURCE_DIR}/cmake/3rd_party.cmake)
endif(PROJECT_IS_IN_ROOT)

if(HAS_BENCHES) 
    include_googletest()
    set(CMAKE_BUILD_TYPE Release)
    include_benchmark()
    message(STATUS "Building benches")
    add_subdirectory(benches)
endif(HAS_BENCHES) 

# The below needs to be built in Debug mode
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g")

if(HAS_TESTS) 
    include_benchmark()
    message(STATUS "Building tests")
    add_subdirectory(tests)
endif(HAS_TESTS)

if(HAS_EXAMPLES) 
    message(STATUS "Building examples")
    add_subdirectory(examples)
endif(HAS_EXAMPLES) 
