---
title: Chapter 7. Flow Control
permalink: /books/cmake-by-examples/chapter-7
---

CMake's if statements are used to conditionally control the flow of the CMake script. Here are some examples of using if statements in CMake:

### `if`

- **Example 1: Basic Condition**

  ```cmake
  set(MY_VARIABLE "some_value")

  if(MY_VARIABLE STREQUAL "some_value")
    ...
  endif()
  ```

- **Example 2: Checking if a Variable is Set**

  ```cmake
  if(DEFINED MY_VARIABLE)
    ...
  endif()
  ```

- **Example 3: Checking if a Variable is True**

  ```cmake
  set(MY_FLAG TRUE)

  if(MY_FLAG)
    ...
  endif()
  ```

- **Example 4: Checking if a Variable is False**

  ```cmake
  set(MY_FLAG FALSE)

  if(NOT MY_FLAG)
    ...
  endif()
  ```

- **Example 5: Testing Numeric Values**

  ```cmake
  set(NUMBER 42)

  if(NUMBER LESS 50)
    ...
  endif()
  ```

- **Example 6: Checking if a File Exists**

  ```cmake
  set(FILE_PATH "path/to/myfile.txt")

  if(EXISTS ${FILE_PATH})
    ...
  endif()
  ```

- **Example 7: Checking the Build Type**

  ```cmake
  if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    ...
  endif()
  ```

- **Example 8: Check the version number**

  ```cmake
  cmake_minimum_required(VERSION 3.10)

  # Check if the CMake version is greater than or equal to 3.15
  if(${CMAKE_VERSION} VERSION_GREATER_EQUAL "3.15")
    ...
  endif()
  ```

### `foreach`

The foreach command in CMake is used to iterate over a list. Here are some examples of using foreach in CMake:

- **Example 1: Iterating Over a List of Strings**

  ```cmake
  set(my_list "apple" "banana" "cherry")

  foreach(fruit ${my_list})
  ...
  endforeach()
  ```

- **Example 2: Iterating Over a List of Numbers**

  ```cmake
  set(number_list 1 2 3 4 5)

  foreach(number ${number_list})
  ...
  endforeach()
  ```

- **Example 3: Iterating Over a Range of Numbers**

  ```cmake
  # Create a list of numbers from 1 to 5
  range(1 5 my_range)

  foreach(number ${my_range})
  ...
  endforeach()
  ```

- **Example 4: Iterating Over Source Files**

  ```cmake
  # Get a list of source files in the current directory
  file(GLOB my_sources "*.cpp")

  foreach(source ${my_sources})
  ...
  endforeach()
  ```

- **Example 5: Iterating Over Directories**

  ```cmake
  # Get a list of subdirectories in the current directory
  file(GLOB my_directories RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *)

  foreach(directory ${my_directories})
  ...
  endforeach()
  ```

- **Example 6: Iterating Over Key-Value Pairs**

  ```cmake
  # Create a list of key-value pairs
  set(my_map "name=John" "age=30" "city=New York")

  foreach(pair ${my_map})
    # Split each pair into key and value
    string(REGEX MATCH "([^=]+)=([^=]*)" _ ${pair})
    set(key "${CMAKE_MATCH_1}")
    set(value "${CMAKE_MATCH_2}")

    message(STATUS "Key: ${key}, Value: ${value}")
  endforeach()
  ```

### `while`

CMake doesn't have a direct while statement like some other programming languages. However, you can achieve similar looping behavior using conditional statements and variable manipulation. Here are a few examples demonstrating while-like constructs in CMake:

- **Example 1: Counting from 1 to 5**

  ```cmake
  set(counter 1)

  while(counter LESS_EQUAL 5)
    message(STATUS "Counter: ${counter}")
    math(EXPR counter "${counter} + 1")
  endwhile()
  ```

- **Example 2: Processing Elements in a List**

  ```cmake
  set(my_list "apple" "banana" "cherry")

  list(LENGTH my_list list_length)
  set(index 0)

  while(index LESS list_length)
    list(GET my_list ${index} current_element)
    message(STATUS "Element at index ${index}: ${current_element}")
    math(EXPR index "${index} + 1")
  endwhile()
  ```

- **Example 3: Performing an Operation Until a Condition is Met**

  ```cmake
  set(value 1)

  while(NOT value EQUAL 100)
    message(STATUS "Current Value: ${value}")
    math(EXPR value "${value} * 2")
  endwhile()
  ```
