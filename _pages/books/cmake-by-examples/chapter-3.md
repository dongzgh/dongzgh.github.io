---
title: Chapter 3. Variables
permalink: /books/cmake-by-examples/chapter-3
---

In CMake, there are primarily two types of variables: **simple variables** and **cache variables**. Additionally, there are some special types of variables that are used for specific purposes.

## 3.1. Simple Variables

Simple variables are the most common type of variables in CMake. They are set using the `set` command and can hold values such as strings, numbers, lists, or paths. Simple variables are local to the scope in which they are defined.

Example of setting a simple variable

```cmake
set(MY_STRING_VARIABLE "Hello, CMake!")
set(MY_NUMERIC_VARIABLE 42)
set(MY_LIST_VARIABLE "item1" "item2" "item3")
set(MY_PATH_VARIABLE "/path/to/some/directory")
```

## 3.2. Cache Variables

Cache variables are a special type of variable that can be cached between CMake runs. They are set using the `set` command with the `CACHE` keyword. Cache variables are often used for user-configurable options or to pass information between different CMake runs.

Example of setting a cache variable

```cmake
set(MY_CACHE_VARIABLE "Default Value" CACHE STRING "Description of the variable")
set(MY_NUMERIC_CACHE_VARIABLE 42 CACHE INTEGER "Description of the variable")
```

Users can modify cache variables using CMake's `-D` option during configuration:

```bash
cmake -DMY_CACHE_VARIABLE="New Value" ..
```

## 3.3. Internal Variables

Internal variables are predefined by CMake and provide information about the build environment, system properties, and build settings. These variables are read-only and cannot be modified by the user or in CMake scripts. Examples include `CMAKE_SOURCE_DIR`, `CMAKE_BINARY_DIR`, `CMAKE_CXX_COMPILER`, etc.

Example of using an internal variable

```cmake
message(STATUS "Source directory: ${CMAKE_SOURCE_DIR}")
```

## 3.4. Environment Variables

Environment variables are variables that are inherited from the environment in which CMake is run. You can access environment variables using the `$ENV{VAR_NAME}` syntax.

Example of using an environment variable

```cmake
set(MY_ENV_VARIABLE $ENV{MY_ENV_VARIABLE})
```

## 3.5. Cache Entries

Cache entries are similar to cache variables but are more explicitly used in the context of defining variables that should be stored in the cache.

Example of using a cache entry

```cmake
set(MY_CACHE_ENTRY "Default Value" CACHE ENTRY "Description of the entry")
```

In summary, while there are different ways to categorize variables in CMake, the primary distinction is between simple variables, which are local to the script, and cache variables, which can be cached between CMake runs. Internal variables and environment variables serve specific purposes in providing information about the build environment and accessing external settings. Cache entries are closely related to cache variables but have slightly different use cases.
