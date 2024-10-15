---
title: Chapter 14. Custom Command
permalink: /books/cmake-by-examples/chapter-14
---

Custom commands in CMake are essential for several reasons:

1. **Automating Repetitive Tasks**: Custom commands can automate tasks that need to be performed frequently, such as generating files, copying resources, or running scripts.

2. **Integrating External Tools**: They allow you to integrate external tools and scripts into the build process, ensuring that all necessary steps are performed automatically.

3. **Custom Build Steps**: Sometimes, the default build steps provided by CMake are not sufficient. Custom commands let you define additional steps that are specific to your project.

4. **File Generation**: They can be used to generate source files, headers, or other resources that are required by the build process but are not part of the source tree.

5. **Post-Build Actions**: Custom commands can specify actions that need to be taken after the build, such as packaging, deployment, or running tests.

6. **Cleaning Up**: They can help in cleaning up generated files or other temporary resources, keeping the build directory clean.

7. **Flexibility**: Custom commands provide flexibility to handle complex build scenarios that are not directly supported by CMake's built-in commands.

By using custom commands, you can ensure that your build process is comprehensive, automated, and tailored to the specific needs of your project.

- **Example 1: Adding a Custom Command to Generate a File**

  ```cmake
  add_custom_command(
    OUTPUT ${CMAKE_BINARY_DIR}/generated_file.txt
    COMMAND ${CMAKE_COMMAND} -E echo "This is a generated file" > ${CMAKE_BINARY_DIR}/generated_file.txt
    COMMENT "Generating a custom file"
  )
  ```

- **Example 2: Adding a Custom Command to Run After Building**

  ```cmake
  add_custom_command(
    TARGET my_target
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_SOURCE_DIR}/input.txt ${CMAKE_BINARY_DIR}/output.txt
    COMMENT "Copying input.txt to output.txt after building"
  )
  ```

- **Example 3: Adding a Custom Command to Clean Up Files**

  ```cmake
  add_custom_target(cleanup
    COMMAND ${CMAKE_COMMAND} -E remove ${CMAKE_BINARY_DIR}/generated_file.txt
    COMMENT "Cleaning up generated files"
  )
  ```

- **Example 4: Adding a Custom Command to Run a Script**

  ```cmake
  add_custom_command(
    OUTPUT ${CMAKE_BINARY_DIR}/script_output.txt
    COMMAND ${CMAKE_COMMAND} -E env python3 ${CMAKE_SOURCE_DIR}/script.py > ${CMAKE_BINARY_DIR}/script_output.txt
    COMMENT "Running a Python script"
  )
  ```

- **Example 5: Adding a Custom Command to Generate a Header File**

  ```cmake
  add_custom_command(
    OUTPUT ${CMAKE_BINARY_DIR}/generated_header.h
    COMMAND ${CMAKE_COMMAND} -E echo "#define GENERATED_HEADER" > ${CMAKE_BINARY_DIR}/generated_header.h
    COMMENT "Generating a custom header file"
  )
  ```
