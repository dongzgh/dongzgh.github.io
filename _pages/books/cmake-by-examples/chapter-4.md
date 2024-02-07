---
title: Chapter 4. Buit-in Functions
permalink: /books/cmake-by-examples/chapter-4
---

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
