cmake_minimum_required (VERSION 2.6)
project (maze)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_BUILD_TYPE Release)

find_package(OpenCV REQUIRED)

find_package(PkgConfig)
pkg_check_modules(YamlCpp yaml-cpp)

include_directories(${YamlCpp_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS} include)

add_library(maze SHARED include/maze.h include/a_star.h
    include/point.h src/point.cpp)
target_link_libraries(maze ${OpenCV_LIBS})

#add_executable(generator src/generator.cpp)
#target_link_libraries(generator maze)

#add_executable(line src/solve_line.cpp)
#target_link_libraries(line maze)

add_executable(solve src/solve_cell.cpp src/solve_line.cpp src/solve_corridor.cpp)
target_link_libraries(solve  maze)

#add_executable(corridor src/solve_corridor.cpp)
#target_link_libraries(corridor maze)
