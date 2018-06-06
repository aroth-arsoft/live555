cmake_minimum_required(VERSION 2.8)

project(live555)

if(MSVC)
    add_definitions(-D_WINSOCK_DEPRECATED_NO_WARNINGS -D_CRT_SECURE_NO_WARNINGS)
else()
    SET(GCC_COVERAGE_COMPILE_FLAGS "-fpermissive") #Why is this needed?
    add_definitions(${GCC_COVERAGE_COMPILE_FLAGS})
endif()

include_directories(BasicUsageEnvironment/include)
include_directories(UsageEnvironment/include)
include_directories(groupsock/include)
include_directories(liveMedia/include)
include_directories(liveMedia)
include_directories(mediaServer/include)
#include_directories(proxyServer/include)

file(GLOB SOURCES "groupsock/*.cpp" "groupsock/*.c"
                  "liveMedia/*.cpp" "liveMedia/*.c"
                  "BasicUsageEnvironment/*.cpp" "BasicUsageEnvironment/*.c"
                  "UsageEnvironment/*.cpp" "UsageEnvironment/*.c"
                  #"mediaServer/*.cpp" "mediaServer/*.c"
) #"proxyServer/*.cpp" "proxyServer/*.c"

add_definitions(-DXLOCALE_NOT_USED)

add_library(live555 SHARED ${SOURCES})

#g++ openRTSP.cpp playCommon.cpp -I . -I ../liveMedia/include -I ../liveMedia -I ../groupsock/include -I ../UsageEnvironment/include -I ../BasicUsageEnvironment/include ../liblive555.so -o openRTSP
#LD_LIBRARY_PATH=../ ./openRTSP

if(WIN32)
    target_link_libraries(live555 PRIVATE ws2_32.lib)
endif()

install(TARGETS live555
        RUNTIME DESTINATION bin)

add_subdirectory(mediaServer)
