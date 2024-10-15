---
title: Chapter 12. Debugging and Profiling
permalink: /books/cmake-by-examples/chapter-12
---

## 12.1 Log Messages

The `message` command in CMake is a useful tool for debugging and providing information during the configuration process. It can be used to print messages to the console at various verbosity levels. Here are some examples of using `message` for debugging in CMake:

- **Example 1: Basic Message**

  ```cmake
  # Basic message
  message("This is a basic message.")
  ```

- **Example 2: Verbose Messages**

  ```cmake
  # Verbose messages
  message(STATUS "This is a status message.")
  message(WARNING "This is a warning message.")
  message(SEND_ERROR "This is an error message.")
  message(FATAL_ERROR "This is a fatal error message.")
  ```

- **Example 3: Printing Variable Values**

  ```cmake
  # Printing variable values
  set(my_variable "Hello, CMake!")
  message(STATUS "The value of my_variable is: ${my_variable}")
  ```

- **Example 4: Message with Generator Expressions**

  ```cmake
  # Message with generator expression
  message(STATUS "Build type is $<CONFIG>")
  ```

- **Example 5: Printing System Information**

  ```cmake
  # Printing system information
  message(STATUS "CMake version: ${CMAKE_VERSION}")
  message(STATUS "System: ${CMAKE_SYSTEM_NAME}")
  message(STATUS "Processor: ${CMAKE_SYSTEM_PROCESSOR}")
  ```

## 12.2 Profiling

Profiling CMake calls can be helpful for understanding the performance characteristics of your CMake configuration process. While CMake itself doesn't have built-in profiling tools, you can use external tools to analyze the time spent in various CMake commands and scripts. Here are some approaches:

- **CMake's `--trace` Option**

  CMake provides a `--trace` option that can be used to trace the execution of CMake commands. This can help identify which commands are taking the most time.

  ```bash
  cmake --trace <path/to/source>
  ```

  This command traces the execution of CMake, and you can redirect the output to a file for further analysis.

- **CMake Profiler**

  The [CMakeProfiler](https://github.com/toeb/cmakepp)is an open-source tool that aims to profile CMake projects. It provides a graphical interface for visualizing the duration of CMake commands.

  To use it, you generally need to clone the repository, build the profiler, and then use it to profile your CMake project.

- **Manual Timing with `message` Statements**

  You can manually insert `message` statements in your CMakeLists.txt files to measure the time taken by specific sections of your configuration process. For example:

  ```cmake
  # CMakeLists.txt
  message(STATUS "Start timing")
  # ... your CMake code ...
  message(STATUS "End timing")
  ```

  This approach gives you a rough idea of where time is being spent but is less precise than dedicated profiling tools.

- **External Profiling Tools**

  Use external profiling tools like `strace`, `ltrace`, or `perf` (on Linux) to analyze system calls and performance.

  ```bash
  strace -o strace.log cmake <path/to/source>
  ```

  ```bash
  perf record cmake <path/to/source>
  ```

  These tools provide a detailed view of system calls and can help identify performance bottlenecks.

- **CMake GUI**

  The CMake GUI can be used to visualize the command flow. Launch the GUI using:

  ```bash
  cmake-gui <path/to/source>
  ```

  While it doesn't provide direct profiling information, it can give you a clear overview of how CMake is processing your project.

Choose the method that best fits your needs and the available tools on your system. Profiling CMake can be useful for optimizing the configuration process, especially in large projects with complex CMakeLists.txt files.
