---
title: Chapter 10. Modules
permalink: /books/cmake-by-examples/chapter-10
---

CMake modules are script files containing reusable functionality that can be included in CMake projects using the `include` command. Modules help organize and encapsulate commonly used code. Here are examples of writing and using CMake modules:

- **Example 1: Writing a CMake Module with Return Value**

  ```cmake
  # MyMathFunctions.cmake

  function(square_number number)
    math(EXPR result "${number} * ${number}")
    set(${ARGV1} ${result} PARENT_SCOPE)
  endfunction()
  ```

- **Example 2: Using the CMake Module with Return Value**

  ```cmake
  # CMakeLists.txt

  cmake_minimum_required(VERSION 3.10)
  project(MyProject)

  # Include the MyMathFunctions module
  include(MyMathFunctions)

  # Call the function and retrieve the result
  set(input_number 5)
  square_number(${input_number} squared_result)
  message(STATUS "Square of ${input_number}: ${squared_result}")

  # Your project configurations go here...
  ```
  