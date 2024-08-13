cmake_minimum_required (VERSION 3.0.0)
project (live555)

if (DEFINED LIVE555BUILD)
	MESSAGE("LIVE555BUILD is ${LIVE555BUILD}")
else ()
	set(LIVE555BUILD "RelWithDebInfo")
endif ()

if (DEFINED VERACODE)
    set (CMAKE_CXX_FLAGS_RELWITHDEBINFO "/MD /Od /NDEBUG")
    set (CMAKE_C_FLAGS_RELWITHDEBINFO "/MD /Od /NDEBUG")
else()
    set(VERACODE 0)
endif()

if (DEFINED VERACODE)
    set (CMAKE_CXX_FLAGS_RELWITHDEBINFO "/MD /Od /NDEBUG")
    set (CMAKE_C_FLAGS_RELWITHDEBINFO "/MD /Od /NDEBUG")
else()
    set(VERACODE 0)
endif()


MESSAGE("LIVE555BUILD = ${LIVE555BUILD}")

#set (CMAKE_CONFIGURATION_TYPES ${LIVE555BUILD})
set (CMAKE_POSITION_INDEPENDENT_CODE ON)
set (CMAKE_CXX_STANDARD 20)


# target

FILE(GLOB LIVE555_SOURCE groupsock/*.c* liveMedia/*.c* UsageEnvironment/*.c* BasicUsageEnvironment/*.c*)
list(FILTER LIVE555_SOURCE EXCLUDE REGEX "liveMedia/RTSPServerSupportingHTTPStreaming.cpp")
SET(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
add_library (${PROJECT_NAME} SHARED ${LIVE555_SOURCE})
target_include_directories(${PROJECT_NAME} PUBLIC groupsock/include liveMedia/include UsageEnvironment/include BasicUsageEnvironment/include OpenSSL/include)
target_link_libraries (${PROJECT_NAME} ws2_32) 

# compiler specific
if (MSVC)
	add_definitions(-DWEBRTC_WIN -DNO_GETIFADDRS -EHsc -DNOMINMAX -D__PRETTY_FUNCTION__=__FUNCTION__ -DNO_OPENSSL)
	set(CompilerFlags CMAKE_CXX_FLAGS_DEBUG CMAKE_C_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE CMAKE_C_FLAGS_RELEASE)
	foreach(CompilerFlag ${CompilerFlags})
	  string(REPLACE "/MT" "/MD" ${CompilerFlag} "${${CompilerFlag}}")
	endforeach()
	
endif(MSVC)

SET(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS OFF)
# live555
set(LIVE555_COMPILER_FLAGS "/wd\"4244\" /wd\"4267\" /wd\"4996\" /wd\"4312\" /wd\"4018\" /wd\"4334\" /wd\"4477\"")
SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${LIVE555_COMPILER_FLAGS}" )
add_definitions(-D_CRT_SECURE_NO_WARNINGS)
if (WIN32)
	SET (SHELLCOMMAND cmd /c )
endif(WIN32)

