# project
cmake_minimum_required (VERSION 3.14)

project (libviso2 LANGUAGES CXX VERSION 2.3)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(PNG REQUIRED)

set(	SOURCES 
	src/matrix.cpp 
	src/triangle.cpp 
	src/filter.cpp 
	src/matcher.cpp 
	src/reconstruction.cpp 
	src/viso.cpp 
	src/viso_mono.cpp 
	src/viso_stereo.cpp
)

add_library(viso2 ${SOURCES})

target_include_directories(viso2 INTERFACE src)

target_compile_options(viso2 PRIVATE -msse3 -w)

add_executable(demo src/demo.cpp)

target_link_libraries (demo viso2 PNG::PNG)

target_compile_options(demo PRIVATE -msse3 -w)

set(CMAKE_BUILD_TYPE Release)
