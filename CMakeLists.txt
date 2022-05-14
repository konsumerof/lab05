cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDART 11)
set(CMAKE_CXX_STANDART _REQUIRED ON)
set(GCC_COVERAGE_COMPILE_FLAGS "-fprofile-arcs -ftest-coverage")
set(CMAKE_CXX_FLAGS "-fprofile-arcs -ftest-coverage")

project(lab05)

include_directories(banking)
add_subdirectory(banking banking)

option(BUILD_TESTS "Build tests" ON)
option(COVERAGE "Coverage" ON)

if(BUILD_TESTS)
 enable_testing()
 add_executable(check tests/tests.cpp)
 add_subdirectory(third-party/gtest)
 target_compile_options(check PRIVATE --coverage)
 target_link_libraries(check banking gtest_main gmock_main --coverage)
 add_test(NAME check COMMAND check)
 endif()
