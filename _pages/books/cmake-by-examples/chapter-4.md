---
title: Chapter 4. Managing Dependencies
permalink: /books/cmake-by-examples/chapter-4
---

## 4.1 `include`  vs. `add_subdirectory`

Both `include` and `add_subdirectory` are CMake commands used for incorporating external CMake files into the current one, but they serve different purposes.

1. **`include` Command:**
   - The `include` command is used to read and execute the content of another CMake script within the current context.
   - It is typically used for including CMake scripts that contain functions or macros that you want to use in the current CMakeLists.txt file.
   - The included script shares the same variable scope as the including script.
   - It is not suitable for bringing in external projects or adding subdirectories with their own CMakeLists.txt files.

   Example of using `include`:

   ```cmake
   # MyProject/CMakeLists.txt
   cmake_minimum_required(VERSION 3.10)
   project(MyProject)

   # Include a helper script
   include(helpers.cmake)

   # Call a function from the included script
   my_function()
   ```

   ```cmake
   # MyProject/helpers.cmake
   function(my_function)
       message(STATUS "Hello from my_function!")
   endfunction()
   ```

2. **`add_subdirectory` Command:**
   - The `add_subdirectory` command is used to add a subdirectory with its own CMakeLists.txt file to the build.
   - It is typically used for including external projects or adding modular components to the current project.
   - The included subdirectory has its own variable scope, and variables defined in the subdirectory do not affect the parent scope unless explicitly exported.
   - `add_subdirectory` can be used to bring in libraries, executables, or other targets defined in the subdirectory.

   Example of using `add_subdirectory`:

   ```cmake
   # MyProject/CMakeLists.txt
   cmake_minimum_required(VERSION 3.10)
   project(MyProject)

   # Add a subdirectory with its own CMakeLists.txt file
   add_subdirectory(subdirectory)

   # Main executable and other configurations...
   ```

   ```cmake
   # MyProject/subdirectory/CMakeLists.txt
   # Subdirectory target
   add_library(MyLibrary my_file.cpp)

   # Add include directories if needed
   target_include_directories(MyLibrary PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
   ```

In summary, use `include` for bringing in CMake scripts within the same project, and use `add_subdirectory` for incorporating external projects or modular components with their own CMakeLists.txt files.
