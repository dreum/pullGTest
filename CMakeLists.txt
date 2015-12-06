cmake_minimum_required(VERSION 2.8)
# Download and unpack gtest at configure time
configure_file(gtest-CMakeLists.txt gtest-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/gtest-download )
execute_process(COMMAND ${CMAKE_COMMAND} --build .
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/gtest-download )
 
# Add gtest directly to our build
add_subdirectory(${CMAKE_BINARY_DIR}/gtest-src
                 ${CMAKE_BINARY_DIR}/gtest-build
                 EXCLUDE_FROM_ALL )
 
# Add the gtest include directory, since gtest
# doesn't add that dependency to its gtest target
target_include_directories(gtest INTERFACE
  "${CMAKE_BINARY_DIR}/gtest-src/include")
project(GTestTutorial)
add_executable(GTestTutorial gtest_runner.cpp)
target_link_libraries(GTestTutorial gtest)
