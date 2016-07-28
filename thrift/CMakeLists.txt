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

set(thrift_src
    gen-cpp/Calculator.cpp
    gen-cpp/SharedService.cpp
    gen-cpp/shared_constants.cpp
    gen-cpp/shared_types.cpp
    gen-cpp/tutorial_constants.cpp
    gen-cpp/tutorial_types.cpp
)

add_custom_command(
	OUTPUT ${thrift_src}
	COMMAND thrift -r --gen cpp ${CMAKE_CURRENT_SOURCE_DIR}/src/tutorial.thrift
)

add_library(net ${thrift_src})
target_link_libraries(net cppan)

add_executable(client src/client.cpp)
target_link_libraries(client net)

add_executable(server src/server.cpp)
target_link_libraries(server net)
