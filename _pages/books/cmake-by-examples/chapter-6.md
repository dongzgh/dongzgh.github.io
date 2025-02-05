---
title: Chapter 6. Functions and Macros
permalink: /books/cmake-by-examples/chapter-6
---

In CMake, you can define and use functions to encapsulate sets of commands and create reusable blocks of code. Here are some examples of how to define and use functions:

- **Example 1: Simple Function**

  ```cmake
  # Define a function
  function(say_hello)
    message(STATUS "Hello from the function!")
  endfunction()

  # Call the function
  say_hello()
  ```

- **Example 2: Function with Parameters**

  ```cmake
  # Define a function with parameters
  function(greet_person person)
    message(STATUS "Hello, ${person}!")
  endfunction()

  # Call the function with a parameter
  greet_person("Alice")
  ```

- **Example 3: Function with Return Value**

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

- **Example 4: Function with Default Parameters**

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

In CMake, both macros and functions serve the purpose of encapsulating and reusing code, but they have some differences scope handling.

- Functions in CMake create their own variable scope. Variables defined or modified inside a function are local to that function unless explicitly marked with PARENT_SCOPE to affect the calling scope.
- Macro in CMake share the same variable scope with the calling context. Variables modified inside a macro directly affect the variables in the calling scope.
