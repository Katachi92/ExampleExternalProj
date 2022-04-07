cmake_minimum_required(VERSION 3.10)

include(ExternalProject)

project(Tutorial)

add_executable(Tutorial tutorial.cpp)

ExternalProject_Add(some_lib
		PREFIX some_lib
		SOURCE_DIR
				${CMAKE_CURRENT_SOURCE_DIR}/tutorial_lib
		CMAKE_CACHE_ARGS
				-DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR>
		)

ExternalProject_Get_Property(some_lib install_dir)
include_directories(${install_dir}/include)

add_library(SomeLib SHARED IMPORTED)
set_target_properties(SomeLib PROPERTIES IMPORTED_LOCATION ${install_dir}/lib/libSomeLib.so)

add_dependencies(Tutorial some_lib)
target_link_libraries(Tutorial SomeLib)

set(CMAKE_CXX_STANDARD 17)
