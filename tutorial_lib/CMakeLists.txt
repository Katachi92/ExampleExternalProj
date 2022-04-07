cmake_minimum_required(VERSION 3.10)

include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 17)

project(SomeLib VERSION 1.0.0 DESCRIPTION "Some example lib")

add_library(SomeLib SHARED
		src/willFooSthForMe.cpp)

set_target_properties(SomeLib PROPERTIES PUBLIC_HEADER inc/willFooSthForMe.h)

target_include_directories(SomeLib PRIVATE inc)
target_include_directories(SomeLib PRIVATE src)

install(TARGETS SomeLib
		LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
		PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
