---
title: Chapter 3. CMake Language
permalink: /books/cmake-by-examples/chapter-3
---

## 3.1 Variables

In CMake, there are primarily two types of variables: **simple variables** and **cache variables**. Additionally, there are some special types of variables that are used for specific purposes.

### 1. Simple Variables

**Simple variables** are the most common type of variables in CMake. They are set using the `set` command and can hold values such as strings, numbers, lists, or paths. Simple variables are local to the scope in which they are defined.

Example of setting a simple variable:

```cmake
set(MY_STRING_VARIABLE "Hello, CMake!")
set(MY_NUMERIC_VARIABLE 42)
set(MY_LIST_VARIABLE "item1" "item2" "item3")
set(MY_PATH_VARIABLE "/path/to/some/directory")
```

### 2. Cache Variables

**Cache variables** are a special type of variable that can be cached between CMake runs. They are set using the `set` command with the `CACHE` keyword. Cache variables are often used for user-configurable options or to pass information between different CMake runs.

Example of setting a cache variable:

```cmake
set(MY_CACHE_VARIABLE "Default Value" CACHE STRING "Description of the variable")
set(MY_NUMERIC_CACHE_VARIABLE 42 CACHE INTEGER "Description of the variable")
```

Users can modify cache variables using CMake's `-D` option during configuration:

```bash
cmake -DMY_CACHE_VARIABLE="New Value" ..
```

### 3. Internal Variables

**Internal variables** are predefined by CMake and provide information about the build environment, system properties, and build settings. These variables are read-only and cannot be modified by the user or in CMake scripts. Examples include `CMAKE_SOURCE_DIR`, `CMAKE_BINARY_DIR`, `CMAKE_CXX_COMPILER`, etc.

Example of using an internal variable:

```cmake
message(STATUS "Source directory: ${CMAKE_SOURCE_DIR}")
```

### 4. Environment Variables

**Environment variables** are variables that are inherited from the environment in which CMake is run. You can access environment variables using the `$ENV{VAR_NAME}` syntax.

Example of using an environment variable:

```cmake
set(MY_ENV_VARIABLE $ENV{MY_ENV_VARIABLE})
```

### 5. Cache Entries

Cache entries are similar to cache variables but are more explicitly used in the context of defining variables that should be stored in the cache.

Example of using a cache entry:

```cmake
set(MY_CACHE_ENTRY "Default Value" CACHE ENTRY "Description of the entry")
```

In summary, while there are different ways to categorize variables in CMake, the primary distinction is between simple variables, which are local to the script, and cache variables, which can be cached between CMake runs. Internal variables and environment variables serve specific purposes in providing information about the build environment and accessing external settings. Cache entries are closely related to cache variables but have slightly different use cases.

## 3.2 Built-in Functions

### String Functions

CMake provides a set of string manipulation commands and functions that allow you to perform various Functions on strings. Here are some examples of string manipulation in CMake:

- Example 1: Concatenating Strings

  ```cmake
  set(STRING1 "Hello")
  set(STRING2 "CMake!")

  # Concatenate two strings
  set(CONCATENATED_STRING "${STRING1} ${STRING2}")

  message(STATUS "Concatenated String: ${CONCATENATED_STRING}")
  ```

- Example 2: Getting Substrings

  ```cmake
  set(FULL_STRING "ThisIsAString")

  # Get a substring starting from index 4
  string(SUBSTRING ${FULL_STRING} 4 -1 SUBSTRING_RESULT)

  message(STATUS "Substring Result: ${SUBSTRING_RESULT}")
  ```

- Example 3: Finding and Replacing Substrings

  ```cmake
  set(INPUT_STRING "ReplaceThisText")

  # Find and replace a substring
  string(REPLACE "ReplaceThis" "WithThat" OUTPUT_STRING ${INPUT_STRING})

  message(STATUS "Output String: ${OUTPUT_STRING}")
  ```

- Example 4: Converting to Uppercase or Lowercase

  ```cmake
  set(LOWERCASE_STRING "lowercase")
  set(UPPERCASE_STRING "UPPERCASE")

  # Convert to uppercase
  string(TOUPPER ${LOWERCASE_STRING} UPPERCASE_RESULT)

  # Convert to lowercase
  string(TOLOWER ${UPPERCASE_STRING} LOWERCASE_RESULT)

  message(STATUS "Uppercase Result: ${UPPERCASE_RESULT}")
  message(STATUS "Lowercase Result: ${LOWERCASE_RESULT}")
  ```

- Example 5: Getting the Length of a String

  ```cmake
  set(STRING_TO_MEASURE "MeasureMe")

  # Get the length of a string
  string(LENGTH ${STRING_TO_MEASURE} STRING_LENGTH)

  message(STATUS "String Length: ${STRING_LENGTH}")
  ```

- Example 6: Trimming Whitespace

  ```cmake
  set(STRING_WITH_WHITESPACE "   Trim Me   ")

  # Remove leading and trailing whitespace
  string(STRIP ${STRING_WITH_WHITESPACE} TRIMMED_STRING)

  message(STATUS "Trimmed String: ${TRIMMED_STRING}")
  ```

### List Functions

CMake provides several commands and functions for manipulating lists. Here are some examples of list Functions in CMake:

- Example 1: Creating a List

  ```cmake
  # Creating a list
  set(MY_LIST item1 item2 item3)

  message(STATUS "My List: ${MY_LIST}")
  ```

- Example 2: Appending to a List

  ```cmake
  # Appending to a list
  set(MY_LIST item1)
  list(APPEND MY_LIST item2 item3)

  message(STATUS "My List: ${MY_LIST}")
  ```

- Example 3: Getting the Length of a List

  ```cmake
  # Getting the length of a list
  list(LENGTH MY_LIST LIST_LENGTH)

  message(STATUS "List Length: ${LIST_LENGTH}")
  ```

- Example 4: Accessing Elements in a List

  ```cmake
  # Accessing elements in a list
  list(GET MY_LIST 0 FIRST_ITEM)
  list(GET MY_LIST 1 SECOND_ITEM)

  message(STATUS "First Item: ${FIRST_ITEM}")
  message(STATUS "Second Item: ${SECOND_ITEM}")
  ```

- Example 5: Iterating Over a List

  ```cmake
  # Iterating over a list
  foreach(item IN LISTS MY_LIST)
      message(STATUS "List Item: ${item}")
  endforeach()
  ```

- Example 6: Concatenating Lists

  ```cmake
  # Concatenating lists
  set(LIST1 item1 item2)
  set(LIST2 item3 item4)

  list(APPEND CONCATENATED_LIST ${LIST1} ${LIST2})

  message(STATUS "Concatenated List: ${CONCATENATED_LIST}")
  ```

- Example 7: Removing Duplicates from a List

  ```cmake
  # Removing duplicates from a list
  set(DUPLICATES_LIST item1 item2 item1 item3)

  list(REMOVE_DUPLICATES DUPLICATES_LIST)

  message(STATUS "List with Duplicates: ${DUPLICATES_LIST}")
  ```

- Example 8: Removing Elements from a List

  ```cmake
  # Removing elements from a list
  list(REMOVE_ITEM MY_LIST item2)

  message(STATUS "My List after removing item2: ${MY_LIST}")
  ```

### Math Functions

CMake provides built-in math functions that you can use in your CMake scripts. Here are some examples of using CMake's math functions:

- Example 1: Basic Arithmetic Functions

  ```cmake
  # Addition
  math(EXPR RESULT_ADD "3 + 5")
  message(STATUS "Addition Result: ${RESULT_ADD}")

  # Subtraction
  math(EXPR RESULT_SUB "10 - 4")
  message(STATUS "Subtraction Result: ${RESULT_SUB}")

  # Multiplication
  math(EXPR RESULT_MUL "6 * 7")
  message(STATUS "Multiplication Result: ${RESULT_MUL}")

  # Division
  math(EXPR RESULT_DIV "100 / 4")
  message(STATUS "Division Result: ${RESULT_DIV}")
  ```

- Example 2: Exponentiation

  ```cmake
  # Exponentiation
  math(EXPR RESULT_POW "2**4")
  message(STATUS "Exponentiation Result: ${RESULT_POW}")
  ```

  - Example 3: Modulo

  ```cmake
  # Modulo
  math(EXPR RESULT_MOD "15 % 7")
  message(STATUS "Modulo Result: ${RESULT_MOD}")
  ```

- Example 4: Absolute Value

  ```cmake
  # Absolute Value
  math(EXPR RESULT_ABS "-42")
  message(STATUS "Absolute Value Result: ${RESULT_ABS}")
  ```

- Example 5: Square Root

  ```cmake
  # Square Root
  math(EXPR RESULT_SQRT "sqrt(25)")
  message(STATUS "Square Root Result: ${RESULT_SQRT}")
  ```

- Example 6: Trigonometric Functions

  ```cmake
  # Sine
  math(EXPR RESULT_SIN "sin(30)")
  message(STATUS "Sine Result: ${RESULT_SIN}")

  # Cosine
  math(EXPR RESULT_COS "cos(60)")
  message(STATUS "Cosine Result: ${RESULT_COS}")
  ```

- Example 7: Random Number

  ```cmake
  # Random Number
  math(RANDOM RAND_RESULT)
  message(STATUS "Random Number: ${RAND_RESULT}")
  ```

- Example 8: Floor and Ceiling

  ```cmake
  # Floor
  math(EXPR RESULT_FLOOR "floor(7.8)")
  message(STATUS "Floor Result: ${RESULT_FLOOR}")

  # Ceiling
  math(EXPR RESULT_CEIL "ceil(3.2)")
  message(STATUS "Ceiling Result: ${RESULT_CEIL}")
  ```

## 3.3 Functions and Macros

In CMake, you can define and use functions to encapsulate sets of commands and create reusable blocks of code. Here are some examples of how to define and use functions:

- Example 1: Simple Function

  ```cmake
  # Define a function
  function(say_hello)
      message(STATUS "Hello from the function!")
  endfunction()

  # Call the function
  say_hello()
  ```

In this example, we define a function `say_hello` that prints a message. We then call this function, resulting in the message "Hello from the function!" being printed during the configuration stage.

- Example 2: Function with Parameters

  ```cmake
  # Define a function with parameters
  function(greet_person person)
      message(STATUS "Hello, ${person}!")
  endfunction()

  # Call the function with a parameter
  greet_person("Alice")
  ```

Here, we define a function `greet_person` that takes a parameter `person` and prints a personalized greeting. We call the function with the parameter "Alice," resulting in the message "Hello, Alice!" being printed.

- Example 3: Function with Return Value

  ```cmake
  # Define a function with a return value
  function(square_number number)
      math(EXPR result "${number} * ${number}")
      set(${ARGV1} ${result} PARENT_SCOPE)
  endfunction()

  # Call the function and retrieve the result
  set(input_number 5)
  square_number(${input_number} squared_result)
  message(STATUS "Square of ${input_number}: ${squared_result}")
  ```

In this example, we define a function `square_number` that takes a parameter `number`, calculates its square, and sets the result as a variable with the name specified in the second argument. We then call the function with the input number 5 and print the squared result.

- Example 4: Function with Default Parameters

  ```cmake
  # Define a function with default parameters
  function(print_message message_type message_text)
      if(NOT DEFINED message_type)
          set(message_type "INFO" PARENT_SCOPE)
      endif()

      message(${message_type} "${message_text}")
  endfunction()

  # Call the function with and without a message type
  print_message("This is an info message.")
  print_message("WARNING" "This is a warning message.")
  ```

Here, we define a function `print_message` that takes two parameters: `message_type` and `message_text`. If `message_type` is not provided, it defaults to "INFO." We then call the function with and without specifying a message type.

These examples demonstrate various aspects of defining and using functions in CMake. Functions in CMake provide a way to modularize your CMake code, making it more readable and maintainable.

In CMake, both macros and functions serve the purpose of encapsulating and reusing code, but they have some differences scope handling.

- Functions in CMake create their own variable scope. Variables defined or modified inside a function are local to that function unless explicitly marked with PARENT_SCOPE to affect the calling scope.
- Macro in CMake share the same variable scope with the calling context. Variables modified inside a macro directly affect the variables in the calling scope.

## 3.4 Flow Control

CMake's if statements are used to conditionally control the flow of the CMake script. Here are some examples of using if statements in CMake:

### `if`

- Example 1: Basic Condition

  ```cmake
  set(MY_VARIABLE "some_value")

  if(MY_VARIABLE STREQUAL "some_value")
    ...
  endif()
  ```

- Example 2: Checking if a Variable is Set

  ```cmake
  if(DEFINED MY_VARIABLE)
    ...
  endif()
  ```

- Example 3: Checking if a Variable is True

  ```cmake
  set(MY_FLAG TRUE)

  if(MY_FLAG)
    ...
  endif()
  ```

- Example 4: Checking if a Variable is False

  ```cmake
  set(MY_FLAG FALSE)

  if(NOT MY_FLAG)
    ...
  endif()
  ```

- Example 5: Testing Numeric Values

  ```cmake
  set(NUMBER 42)

  if(NUMBER LESS 50)
    ...
  endif()
  ```

- Example 6: Checking if a File Exists

  ```cmake
  set(FILE_PATH "path/to/myfile.txt")

  if(EXISTS ${FILE_PATH})
    ...
  endif()
  ```

- Example 7: Checking the Build Type

  ```cmake
  if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    ...
  endif()
  ```

- Example 8: Check the version number

  ```cmake
  cmake_minimum_required(VERSION 3.10)

  # Check if the CMake version is greater than or equal to 3.15
  if(${CMAKE_VERSION} VERSION_GREATER_EQUAL "3.15")
    ...
  endif()
  ```

### `foreach`

The foreach command in CMake is used to iterate over a list. Here are some examples of using foreach in CMake:

- Example 1: Iterating Over a List of Strings

  ```cmake
  set(my_list "apple" "banana" "cherry")

  foreach(fruit ${my_list})
  ...
  endforeach()
  ```

- Example 2: Iterating Over a List of Numbers

  ```cmake
  set(number_list 1 2 3 4 5)

  foreach(number ${number_list})
  ...
  endforeach()
  ```

- Example 3: Iterating Over a Range of Numbers

  ```cmake
  # Create a list of numbers from 1 to 5
  range(1 5 my_range)

  foreach(number ${my_range})
  ...
  endforeach()
  ```

- Example 4: Iterating Over Source Files

  ```cmake
  # Get a list of source files in the current directory
  file(GLOB my_sources "*.cpp")

  foreach(source ${my_sources})
  ...
  endforeach()
  ```

- Example 5: Iterating Over Directories

  ```cmake
  # Get a list of subdirectories in the current directory
  file(GLOB my_directories RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *)

  foreach(directory ${my_directories})
  ...
  endforeach()
  ```

- Example 6: Iterating Over Key-Value Pairs

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

- Example 1: Counting from 1 to 5

  ```cmake
  set(counter 1)

  while(counter LESS_EQUAL 5)
      message(STATUS "Counter: ${counter}")
      math(EXPR counter "${counter} + 1")
  endwhile()
  ```

- Example 2: Processing Elements in a List

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

- Example 3: Performing an Operation Until a Condition is Met

  ```cmake
  set(value 1)

  while(NOT value EQUAL 100)
      message(STATUS "Current Value: ${value}")
      math(EXPR value "${value} * 2")
  endwhile()
  ```

## 3.5 Properties

In CMake, properties are a way to attach extra information to targets, source files, or directories. Here are some examples of how to set and get CMake properties:

- Example 1: Setting and Getting Target Properties

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

In this example, we set properties for the target `MyExecutable` using `set_target_properties`. We set the C++ standard to 11, require it, and specify the output name. We then use `get_target_property` to retrieve and print the output name.

- Example 2: Setting and Getting Source File Properties

  ```cmake
  # Setting properties for a source file
  set_source_files_properties(main.cpp PROPERTIES
      COMPILE_DEFINITIONS "ENABLE_FEATURE_X"
  )

  # Getting properties of a source file
  get_source_file_property(definitions main.cpp COMPILE_DEFINITIONS)
  message(STATUS "Compile Definitions for main.cpp: ${definitions}")
  ```

In this example, we set properties for the source file `main.cpp` using `set_source_files_properties`. We define a compile definition, and then use `get_source_file_property` to retrieve and print the compile definitions.

- Example 3: Setting and Getting Directory Properties

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

In this example, we set properties for the current directory using `set_directory_properties`. We set a version number and documentation path. We then use `get_directory_property` to retrieve and print these properties.

These examples demonstrate how to set and get properties for targets, source files, and directories in CMake. Properties provide a flexible way to configure various aspects of your CMake project.

## 3.6 Generator Expressions

Generator expressions in CMake provide a way to customize build configurations and settings based on the build system generator. They are used within CMake commands and properties to conditionally specify values based on the generator in use. Here are some examples of how to use generator expressions:

- Example 1: Setting Compiler Flags Conditionally

  ```cmake
  # Set different compiler flags based on the generator
  target_compile_options(MyTarget PRIVATE
      $<$<CXX_COMPILER_ID:MSVC>:/W4>
      $<$<CXX_COMPILER_ID:GNU>:-Wall>
      $<$<CXX_COMPILER_ID:Clang>:-Wall>
  )
  ```

In this example, the `target_compile_options` command sets different compiler warning flags based on the compiler in use. For MSVC, it sets `/W4`; for GCC and Clang, it sets `-Wall`.

- Example 2: Conditionally Linking Libraries

  ```cmake
  # Link different libraries based on the generator
  target_link_libraries(MyTarget PRIVATE
      $<$<CONFIG:Debug>:debug_library>
      $<$<CONFIG:Release>:optimized release_library>
  )
  ```

Here, the `target_link_libraries` command conditionally links different libraries based on the build configuration. For the Debug configuration, it links `debug_library`; for the Release configuration, it links the optimized version of `release_library`.

- Example 3: Adding Compile Definitions Conditionally

  ```cmake
  # Add compile definitions based on the generator
  target_compile_definitions(MyTarget PRIVATE
      $<$<CONFIG:Debug>:DEBUG_MODE>
      $<$<CONFIG:Release>:RELEASE_MODE>
  )
  ```

In this example, the `target_compile_definitions` command adds compile definitions based on the build configuration. For the Debug configuration, it adds `DEBUG_MODE`; for the Release configuration, it adds `RELEASE_MODE`.

- Example 4: Configuring Output Paths Conditionally

  ```cmake
  # Configure output paths based on the generator
  set_target_properties(MyTarget PROPERTIES
      RUNTIME_OUTPUT_DIRECTORY $<$<CONFIG:Debug>:${CMAKE_BINARY_DIR}/bin/debug>
      RUNTIME_OUTPUT_DIRECTORY $<$<CONFIG:Release>:${CMAKE_BINARY_DIR}/bin/release>
  )
  ```

Here, the `set_target_properties` command configures different output paths based on the build configuration. For the Debug configuration, it sets the output directory to `${CMAKE_BINARY_DIR}/bin/debug`; for the Release configuration, it sets it to `${CMAKE_BINARY_DIR}/bin/release`.

These examples demonstrate how generator expressions can be used to conditionally set values based on the build system generator or build configuration in CMake. They provide flexibility in configuring different aspects of the build depending on the context.
