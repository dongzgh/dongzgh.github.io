---
title: Chapter 8. Properties
permalink: /books/cmake-by-examples/chapter-8
---

In CMake, properties are a way to attach extra information to targets, source files, or directories. Here are some examples of how to set and get CMake properties:

- **Example 1: Setting and Getting Target Properties**

  ```cmake
  # Setting properties for a target
  add_executable(MyExecutable main.cpp)
  set_target_properties(MyExecutable PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED ON
    OUTPUT_NAME "MyApp"
  )

  # Getting properties of a target
  get_target_property(output_name MyExecutable OUTPUT_NAME)
  message(STATUS "Output Name of MyExecutable: ${output_name}")
  ```

- **Example 2: Setting and Getting Source File Properties**

  ```cmake
  # Setting properties for a source file
  set_source_files_properties(main.cpp PROPERTIES
    COMPILE_DEFINITIONS "ENABLE_FEATURE_X"
  )

  # Getting properties of a source file
  get_source_file_property(definitions main.cpp COMPILE_DEFINITIONS)
  message(STATUS "Compile Definitions for main.cpp: ${definitions}")
  ```

- **Example 3: Setting and Getting Directory Properties**

  ```cmake
  # Setting properties for a directory
  set_directory_properties(PROPERTIES
    VERSION 1.2.3
    DOCUMENTATION "Path to documentation"
  )

  # Getting properties of a directory
  get_directory_property(version_value DIRECTORY PROPERTY VERSION)
  get_directory_property(documentation_path DIRECTORY PROPERTY DOCUMENTATION)
  message(STATUS "Version: ${version_value}")
  message(STATUS "Documentation Path: ${documentation_path}")
  ```
