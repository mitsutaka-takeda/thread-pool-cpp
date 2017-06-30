cmake_minimum_required(VERSION 3.6)

project(thread-pool-cpp CXX)

option(TESTS "Enable testing" ON)
option(INSTALL "Enable install option" OFF)
option(COVERAGE "Enable code coverage" OFF)
option(BENCHMARK "Build benchmark" ON)

# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wextra -Wsign-compare")

add_library(ThreadPoolCpp INTERFACE)

add_library(ThreadPoolCpp::ThreadPoolCpp ALIAS ThreadPoolCpp)

target_include_directories(
  ThreadPoolCpp
  INTERFACE
  include
  )

target_compile_options(
  ThreadPoolCpp
  INTERFACE
  -std=c++11
  )

if(COVERAGE)
  target_compile_options(
    ThreadPoolCpp
    INTERFACE
    -g 
    --coverage
    )
  
  target_link_libraries(
    ThreadPoolCpp
    INTERFACE
    --coverage
    )
endif()


# gtest
if(TESTS)
  # Tests
  enable_testing()
  add_subdirectory(tests)
endif()



# Benchmark
if(BENCHMARK)
  add_subdirectory(benchmark)
endif()

if(INSTALL)
  # Install
  file(GLOB_RECURSE INSTALL_FILES_LIST "${CMAKE_CURRENT_SOURCE_DIR}/include/*")
  set_source_files_properties(${INSTALL_FILES_LIST} PROPERTIES HEADER_FILE_ONLY 1)
  add_library(HEADER_ONLY_TARGET STATIC ${INSTALL_FILES_LIST})
  set_target_properties(HEADER_ONLY_TARGET PROPERTIES LINKER_LANGUAGE CXX)
  install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/include/" DESTINATION "include")
endif()
