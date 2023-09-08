cmake_minimum_required(VERSION 3.27)
project(gcc_container VERSION 0.1.0 LANGUAGES C CXX)
set (CMAKE_CXX_STANDARD 23)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(fmt REQUIRED)

add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} PRIVATE ${fmt_LIBRARIES})
include_directories(${PROJECT_NAME} PRIVATE ${fmt_INCLUDE_DIRS})
