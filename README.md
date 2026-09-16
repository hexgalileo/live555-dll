![Hexagon logo](/Hexagon_RGB.jpg)

# live555-dll
Windows DLL build of Live555 based on the 2022-12-01 release from live555.com/liveMedia to meet LGPL requirements

# Build Instructions
To build this DLL, perform the following steps:
1. Pull the code.
2. Open a Developer Command Prompt and run: cmake -D LIVE555BUILD="Release" -G "Visual Studio 17 2022" -A x64 .
3. Open the live555.sln file with Visual Studio 2022 and build live555

NOTE: The C++ compiler must be enabled in Visual Studio.

For the latest version of Live555 Streaming Media and corresponding license information, go to [LIVE555 Streaming Media](http://www.live555.com/liveMedia/).

Hexagon Safety, Infrastructure & Geospatial is a division of Hexagon.
