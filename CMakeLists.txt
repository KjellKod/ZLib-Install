cmake_minimum_required(VERSION 3.2)

project(zlibinstall)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_BUILD_TYPE Release)


# include(ExternalProject)
# externalproject_add(g3log
#   URL              https://github.com/KjellKod/g3log/archive/c++11-master.zip
#   SOURCE_DIR       "${G3LOG_SOURCE_DIR}"
#   BINARY_DIR       "${G3LOG_BINARY_DIR}"
#   CMAKE_ARGS       -DG3_SHARED_LIB=OFF -DCMAKE_POSITION_INDEPENDENT_CODE=ON -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE} -DCMAKE_MACOSX_RPATH=1 -DADD_FATAL_EXAMPLE=OFF -DUSE_DYNAMIC_LOGGING_LEVELS=ON
#   INSTALL_COMMAND  ""
#   )




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
else()
  message("successful --------->")
endif()
