cmake_minimum_required(VERSION 2.8)

project(basicUsageEnvironment)

SET(GCC_COVERAGE_COMPILE_FLAGS "-fpermissive") #Why is this needed?
add_definitions(${GCC_COVERAGE_COMPILE_FLAGS})

include_directories(include)
include_directories(../UsageEnvironment/include)
include_directories(../groupsock/include)

#add_definitions(-DXLOCALE_NOT_USED)

file(GLOB SOURCES "*.cpp" "*.c") 

add_library(basicUsageEnvironment SHARED ${SOURCES})
