cmake_minimum_required(VERSION 3.27)
project(gcc_container VERSION 0.1.0 LANGUAGES C CXX)
set (CMAKE_CXX_STANDARD 23)

add_executable(${PROJECT_NAME} main.cpp)