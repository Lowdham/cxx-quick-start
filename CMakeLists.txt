# set cmake version requirement
cmake_minimum_required(VERSION 3.10) 

# set the project name 
# project(YOUR_PROJECT_NAME)

# set the standard
# set(CMAKE_CXX_STANDARD 17) 
# set(CMAKE_CXX_STANDARD_REQUIRED True)

# get the argument.
option(BENCHMARK "option for benchmark" OFF)
option(TEST "option for test" OFF)

# add_subdirectory(${PROJECT_SOURCE_DIR}/YOUR_LIBRARY)

#
# add_subdirectory(${PROJECT_SOURCE_DIR}/dependencies/googletest-release-1.11.0)
# include_directories(${PROJECT_SOURCE_DIR}/dependencies/googletest-release-1.11.0/googletest/include)
# set(BENCHMARK_ENABLE_TESTING OFF)

# test
if(TEST)

  # enable_testing()

  # add_executable(YOUR_EXECUTABLE ${PROJECT_SOURCE_DIR}/YOUR_SOURCE_FILE)

  # target_link_libraries(YOUR_EXECUTABLE gtest gtest_main YOUR_LIBRARY)

  # add_test(NAME YOUR_EXECUTABLE COMMAND YOUR_EXECUTABLE)
endif()


# benchmark
if(BENCHMARK)

  set(DBENCHMARK_ENABLE_LTO true)
  set(BENCHMARK_PATH ${CMAKE_CURRENT_SOURCE_DIR}/benchmark/${CMAKE_SYSTEM_NAME})
  add_subdirectory(dependencies/benchmark-1.5.6)
  include_directories(dependencies/benchmark-1.5.6/include)


  # Get the benchmark files and generate benchmark.
  set(BENCHMARK_SRC_LIST)
  file(GLOB BENCHMARK_SRC_LIST ${PROJECT_SOURCE_DIR}/YOUR_BENCHMARK_SOURCE_FILE)
  foreach(SRC_FILE_PATH ${BENCHMARK_SRC_LIST})
    STRING(REGEX REPLACE ".+/(.+)\\..*" "\\1" SRC_FILE_NAME ${SRC_FILE_PATH})
    # compile
    add_executable(${SRC_FILE_NAME} ${SRC_FILE_PATH})
    # link
    target_link_libraries(${SRC_FILE_NAME} benchmark benchmark_main YOUR_LIBRARY)
  endforeach(SRC_FILE_PATH)

endif()