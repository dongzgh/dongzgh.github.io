---
title: Chapter 4. Configurations
permalink: /books/cmake-by-examples/chapter-4
---

In CMake, you can configure header files by using the `configure_file` function. This function allows you to replace variables in a template header file during the CMake configuration step. This is useful when you want to embed version numbers, compilation options, or other information into your code at build time.

- **Example 1: Simple Version Information in Header**

   ```c
   // config.h.in
   #define PROJECT_VERSION_MAJOR @PROJECT_VERSION_MAJOR@
   #define PROJECT_VERSION_MINOR @PROJECT_VERSION_MINOR@
   ```

   ```cmake
   # CMakeLists.txt
   cmake_minimum_required(VERSION 3.10)
   project(MyProject VERSION 1.0)

   # Configure a header file to pass the version number
   configure_file(
      "${PROJECT_SOURCE_DIR}/config.h.in"
      "${PROJECT_BINARY_DIR}/config.h"
   )

   # Include the binary directory so the configured header is found
   include_directories("${PROJECT_BINARY_DIR}")

   add_executable(MyApp main.cpp)
   ```

   ```c
   // config.h
   #define PROJECT_VERSION_MAJOR 1
   #define PROJECT_VERSION_MINOR 0
   ```

- **Example 2: Configuring a Feature Flag**

   ```c
   // config.h.in
   #define ENABLE_FEATURE @ENABLE_FEATURE@
   ```

   ```cmake
   # CMakeLists.txt
   cmake_minimum_required(VERSION 3.10)
   project(MyProject)

   # Option to enable or disable a feature
   option(ENABLE_FEATURE "Enable a special feature" ON)

   # Configure the header file
   configure_file(
      "${PROJECT_SOURCE_DIR}/config.h.in"
      "${PROJECT_BINARY_DIR}/config.h"
   )

   # Pass a value to the template based on the option
   if(ENABLE_FEATURE)
      set(ENABLE_FEATURE_VALUE 1)
   else()
      set(ENABLE_FEATURE_VALUE 0)
   endif()

   # Configure a header file
   configure_file(
      "${PROJECT_SOURCE_DIR}/config.h.in"
      "${PROJECT_BINARY_DIR}/config.h"
      @ONLY
   )

   # Include the binary directory so the configured header is found
   include_directories("${PROJECT_BINARY_DIR}")

   add_executable(MyApp main.cpp)
   ```

   ```c
   // config.h
   #define ENABLE_FEATURE 1
   // If you disable the feature (`-DENABLE_FEATURE=OFF`), then
   // #define ENABLE_FEATURE 0

   ```

- **Example 3: Including Build Timestamp in Header**

   ```c
   // config.h.in
   #define BUILD_TIMESTAMP "@BUILD_TIMESTAMP@"
   ```

   ```cmake
   # CMakeLists.txt
   cmake_minimum_required(VERSION 3.10)
   project(MyProject)

   # Get the current timestamp
   string(TIMESTAMP BUILD_TIMESTAMP "%Y-%m-%d %H:%M:%S")

   # Configure a header file with the build timestamp
   configure_file(
   "${PROJECT_SOURCE_DIR}/config.h.in"
   "${PROJECT_BINARY_DIR}/config.h"
   )

   # Include the binary directory so the configured header is found
   include_directories("${PROJECT_BINARY_DIR}")

   add_executable(MyApp main.cpp)
   ```

   ```c
   // config.h
   #define BUILD_TIMESTAMP "2024-10-11 12:34:56"
   ```

In all of these examples, the `configure_file` function is key to replacing placeholders in a header template with actual values during the CMake configuration process. You can configure version numbers, feature flags, build timestamps, and other useful information this way. Just ensure that you include the generated header file directory in your include paths using `include_directories("${PROJECT_BINARY_DIR}")`.
