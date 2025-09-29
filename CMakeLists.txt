cmake_minimum_required(VERSION 3.15)
project(nedclib LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_TOOLS "Build command-line tools" ON)

# Add the library subproject
add_subdirectory(src/lib)

# Optionally create executables that link the library
if(BUILD_TOOLS)
  foreach(EXE nedcenc nedcmake nevpk raw2bmp)
    add_executable(${EXE} src/${EXE}.cpp)
    target_link_libraries(${EXE} PRIVATE nedclib)
  endforeach()
endif()
