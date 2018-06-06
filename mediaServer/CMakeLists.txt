include_directories(../BasicUsageEnvironment/include)
include_directories(../UsageEnvironment/include)
include_directories(../liveMedia/include)
include_directories(../groupsock/include)

#add_definitions(-DXLOCALE_NOT_USED)

file(GLOB SOURCES "*.cpp" "*.c") 

add_executable(mediaServer ${SOURCES})

#g++ openRTSP.cpp playCommon.cpp -I . -I ../liveMedia/include -I ../liveMedia -I ../groupsock/include -I ../UsageEnvironment/include -I ../BasicUsageEnvironment/include ../liblive555.so -o openRTSP
#LD_LIBRARY_PATH=../ ./openRTSP

target_link_libraries(mediaServer PRIVATE live555)

install(TARGETS mediaServer
        RUNTIME DESTINATION bin)

