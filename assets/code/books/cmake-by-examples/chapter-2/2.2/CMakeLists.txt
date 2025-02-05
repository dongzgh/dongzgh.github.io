# MyProject/CMakeLists.txt
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# Source files
set(SOURCES src/main.cpp src/my_class.cpp)

# Include directories
include_directories(include)

# Add subdirectories for the main project and external library
add_subdirectory(external/MyLibrary)

# Main application target
add_executable(MyExecutable ${SOURCES})

# Link the executable with the MyLibrary target
target_link_libraries(MyExecutable PRIVATE MyLibrary)
