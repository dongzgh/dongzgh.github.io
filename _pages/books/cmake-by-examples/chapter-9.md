---
title: Chapter 9. Generator Expressions
permalink: /books/cmake-by-examples/chapter-9
---

Generator expressions in CMake provide a way to customize build configurations and settings based on the build system generator. They are used within CMake commands and properties to conditionally specify values based on the generator in use. Here are some examples of how to use generator expressions:

- **Example 1: Setting Compiler Flags Conditionally**

  ```cmake
  # Set different compiler flags based on the generator
  target_compile_options(MyTarget PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>:/W4>
    $<$<CXX_COMPILER_ID:GNU>:-Wall>
    $<$<CXX_COMPILER_ID:Clang>:-Wall>
  )
  ```

- **Example 2: Conditionally Linking Libraries**

  ```cmake
  # Link different libraries based on the generator
  target_link_libraries(MyTarget PRIVATE
    $<$<CONFIG:Debug>:debug_library>
    $<$<CONFIG:Release>:optimized release_library>
  )
  ```

- **Example 3: Adding Compile Definitions Conditionally**

  ```cmake
  # Add compile definitions based on the generator
  target_compile_definitions(MyTarget PRIVATE
    $<$<CONFIG:Debug>:DEBUG_MODE>
    $<$<CONFIG:Release>:RELEASE_MODE>
  )
  ```

- **Example 4: Configuring Output Paths Conditionally**

  ```cmake
  # Configure output paths based on the generator
  set_target_properties(MyTarget PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY $<$<CONFIG:Debug>:${CMAKE_BINARY_DIR}/bin/debug>
    RUNTIME_OUTPUT_DIRECTORY $<$<CONFIG:Release>:${CMAKE_BINARY_DIR}/bin/release>
  )
  ```
