#
# demo_project
#

cmake_minimum_required(VERSION 2.8.12)

# Use solution folders.
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set_property(GLOBAL PROPERTY PREDEFINED_TARGETS_FOLDER "CMake Targets")

project(demo_project C CXX)

# Output directory settings
set(output_dir ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${output_dir})

if (MSVC)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /MP")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP")
endif()

#set(CPPAN_BUILD_SHARED_LIBS ON)
add_subdirectory(cppan)

include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_custom_command(
	OUTPUT addressbook.pb.cc addressbook.pb.h
	COMMAND protoc
	ARGS --cpp_out ${CMAKE_CURRENT_BINARY_DIR} -I ${CMAKE_CURRENT_SOURCE_DIR}/src ${CMAKE_CURRENT_SOURCE_DIR}/src/addressbook.proto
)

add_executable(main src/main.cpp
    addressbook.pb.cc
	addressbook.pb.h)
target_link_libraries(main cppan)
