---
title: Chapter 10. Visibility
permalink: /books/cmake-by-examples/chapter-10
---

In CMake, the visibility of a dependency for a target is controlled using `PUBLIC`, `PRIVATE`, or `INTERFACE` when linking libraries or setting target properties. Here's a breakdown of what each of these keywords means:

- `PUBLIC`: The dependency is used both by the target itself and by any other target that links to this target.
- `PRIVATE`: The dependency is used only by the target itself, not by other targets linking to this target.
- `INTERFACE`: The dependency is not used by the target itself but is used by other targets that link to this target.

Let's look at some examples to clarify how this works.

- **Example 1: `PRIVATE`**

  When a library is needed only by a single target and should not be exposed to anything linking to it, you use `PRIVATE`.

  ```cmake
  add_library(MyLibrary src.cpp)

  # Link MyLibrary with a dependency library called DepLibrary privately
  target_link_libraries(MyLibrary PRIVATE DepLibrary)
  ```

  Here, `DepLibrary` is only needed for compiling and linking `MyLibrary` itself. Any targets that link to `MyLibrary` won't know about or inherit the `DepLibrary` dependency.

- **Example 2: `PUBLIC`**

  When a library is used by the target and should also be inherited by anything linking to that target, use `PUBLIC`.

  ```cmake
  add_library(MyLibrary src.cpp)

  # Link MyLibrary with a dependency library called DepLibrary publicly
  target_link_libraries(MyLibrary PUBLIC DepLibrary)
  ```

  In this case, any target that links to `MyLibrary` will also link to `DepLibrary` because the dependency is public. The headers and compile options required by `DepLibrary` will propagate to any target that depends on `MyLibrary`.

- **Example 3: `INTERFACE`**

  When a target doesn’t use a dependency directly, but anything that links to it should, use `INTERFACE`.

  ```cmake
  add_library(MyLibrary INTERFACE)

  # Specify that anything linking to MyLibrary also links to DepLibrary
  target_link_libraries(MyLibrary INTERFACE DepLibrary)
  ```

  Here, `MyLibrary` doesn't actually need to link against `DepLibrary`, but anything else that links to `MyLibrary` will need `DepLibrary`.

- **Example 4: `target_include_directories` with Visibility**

  You can also control the visibility of include directories in a similar way.

  ```cmake
  add_library(MyLibrary src.cpp)

  # Include directories only used internally by MyLibrary
  target_include_directories(MyLibrary PRIVATE include/private)

  # Include directories that are exposed to consumers of MyLibrary
  target_include_directories(MyLibrary PUBLIC include/public)
  ```

  In this case:

  - The headers in `include/private` are only available when compiling `MyLibrary`.
  - The headers in `include/public` are available to anything that links to `MyLibrary`.
