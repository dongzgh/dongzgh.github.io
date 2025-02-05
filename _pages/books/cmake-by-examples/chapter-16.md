---
title: Chapter 16. Install
permalink: /books/cmake-by-examples/chapter-16
---

## 15.1 Build Install

The `install` target in CMake is a special target that, when invoked, executes the installation rules specified in your `CMakeLists.txt` file. These rules are defined using the `install` command and determine how and where the built files (executables, libraries, headers, etc.) are copied to the installation directories.

- **Example 1: Basic Installation of Executable and Libraries**

  ```cmake
  # Define the executable
  add_executable(my_executable main.cpp)

  # Define the library
  add_library(my_library my_library.cpp)

  # Specify installation rules
  install(TARGETS my_executable my_library
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib/static)
  ```

- **Example 2: Installing Header Files**

  ```cmake
  # Define the library
  add_library(my_library my_library.cpp)

  # Specify installation rules for the library
  install(TARGETS my_library
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib/static)

  # Specify installation rules for header files
  install(FILES my_library.h DESTINATION include)
  ```

- **Example 3: Installing Configuration Files**

  ```cmake
  # Define the executable
  add_executable(my_executable main.cpp)

  # Specify installation rules for the executable
  install(TARGETS my_executable
    RUNTIME DESTINATION bin)

  # Specify installation rules for configuration files
  install(FILES config/my_config.conf DESTINATION etc/my_project)
  ```

- **Example 4: Using `install(DIRECTORY)` to Install a Directory**

  ```cmake
  # Define the executable
  add_executable(my_executable main.cpp)

  # Specify installation rules for the executable
  install(TARGETS my_executable
  RUNTIME DESTINATION bin)

  # Specify installation rules for an entire directory
  install(DIRECTORY resources/ DESTINATION share/my_project/resources)
  ```

- **Example 5: Installing with Component-Based Installation**

  ```cmake
  # Define the executable
  add_executable(my_executable main.cpp)

  # Specify installation rules with components
  install(TARGETS my_executable
    RUNTIME DESTINATION bin
    COMPONENT Runtime)

  install(FILES my_library.h
    DESTINATION include
    COMPONENT Development)

  install(FILES config/my_config.conf
    DESTINATION etc/my_project
    COMPONENT Configuration)
  ```

## 15.2 Run Install

To run the `install` target in CMake, follow these steps:

1. **Configure the Project**: First, you need to configure your project using `cmake`to generate the build system files.

2. **Build the Project**: Build the project using the generated build system.

3. **Run the Install Target**: Finally, run the `install` target to install the files as specified in your `CMakeLists.txt`.

Example command:

```sh
cd my_project
cmake -S . -B build
cmake --build build
cmake --install build
```
