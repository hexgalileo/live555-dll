cmake_minimum_required (VERSION 3.0.0)
project (live555)

FILE(GLOB LIVE555_SOURCE groupsock/*.c* liveMedia/*.c* UsageEnvironment/*.c* BasicUsageEnvironment/*.c*)
SET(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
add_library (live555 SHARED ${LIVE555_SOURCE})	
target_include_directories(live555 PUBLIC groupsock/include liveMedia/include UsageEnvironment/include BasicUsageEnvironment/include)
target_link_libraries (${PROJECT_NAME} ws2_32)

