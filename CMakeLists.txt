cmake_minimum_required(VERSION 3.2)

project(zlib-install)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_BUILD_TYPE Release)

# Google test setup ref: 
# https://github.com/google/googletest/blob/master/googletest/README.md#incorporating-into-an-existing-cmake-project
configure_file(CMakeLists.txt.in zlib-download/CMakeLists.txt)

execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
  RESULT_VARIABLE result 
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/zlib-download )
if(result)
  message(FATAL_ERROR "CMake step for zlib failed: ${result}")
endif()

execute_process(COMMAND ${CMAKE_COMMAND} --build .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/zlib-download )
if(result)
  message(FATAL_ERROR "Build step for zlib failed: ${result}")
endif()