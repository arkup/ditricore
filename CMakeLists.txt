cmake_minimum_required(VERSION 3.2)
project(elfparse)

set(CMAKE_BUILD_TYPE Debug)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -fno-omit-frame-pointer")

#SET(DEBUG_LINK_FLAGS "-fsanitize=address")

#add_definitions(${DEBUG_LINK_FLAGS})

#SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${DEBUG_LINK_FLAGS}" )

set(CMAKE_VERBOSE_MAKEFILE ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

include_directories(src)

add_subdirectory(src)

add_library(capstone STATIC IMPORTED)

set(SOURCE_FILES ${CMAKE_SOURCE_DIR}/src/util/cmdline.h main.cpp)

add_executable(ditricore ${SOURCE_FILES} main.cpp)

add_dependencies(ditricore elf++ dwarf++ disasm capstone)

target_link_libraries(ditricore ${CMAKE_SOURCE_DIR}/lib/libelf++.a)
target_link_libraries(ditricore ${CMAKE_SOURCE_DIR}/lib/libdwarf++.a)
target_link_libraries(ditricore ${CMAKE_SOURCE_DIR}/lib/libdisasm.a)
target_link_libraries(ditricore /usr/lib/libcapstone.a)

