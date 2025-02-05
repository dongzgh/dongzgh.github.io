---
title: Chapter 2. Getting Started with CMake
permalink: /books/cmake-by-examples/chapter-2
---

## 2.1 Creating Your First CMake Project

Creating a basic CMake project involves creating a project directory, adding source code files, and creating a `CMakeLists.txt` file to describe how the project should be built. Here's a simple example of a CMake project for a C++ program:

### 2.1.1. **Project Directory Structure**

Create a project directory and navigate to it:

```bash
mkdir MyProject
cd MyProject
```

### 2.1.2. **Source Code**

Create a C++ source code file, for example, `main.cpp`:

```cpp
// main.cpp
#include <iostream>

int main() {
  std::cout << "Hello, CMake!\n";
  return 0;
}
```

### 2.1.3. **CMakeLists.txt**

Create a `CMakeLists.txt` file in the project directory:

```cmake
# CMakeLists.txt
cmake_minimum_required(VERSION 3.10)

# Project name
project(MyProject)

# Add the executable
add_executable(MyExecutable main.cpp)
```

### 2.1.4. **Build the Project**

Open a terminal in the project directory and run the following commands:

```bash
mkdir build
cd build
cmake ..
make # or use `cmake --build .`
```

These commands create a `build` directory, generate the build files using CMake, and then build the executable using the generated build files.

### 2.1.5. **Run the Executable**

After building the project, you can run the executable:

```bash
./MyExecutable
```

You should see the output: "Hello, CMake!"

This is a very basic example, but it demonstrates the essential steps for creating a CMake project. As your project grows, you can extend the `CMakeLists.txt` file to handle more complex configurations, dependencies, and custom build settings.

## 2.2 Project Structure and Best Practices

Below is an example of how CMake project files can be organized for a simple C++ project. This structure includes separate directories for source code, headers, external libraries, build artifacts, and CMake-related files:

```text
├── bin
├── CMakeLists.txt
├── external
│   └── MyLibrary
│       ├── CMakeLists.txt
│       ├── include
│       │   └── my_library.h
│       └── src
│           └── my_library.cpp
├── include
│   └── my_class.h
├── README.md
└── src
    ├── main.cpp
    └── my_class.cpp
```

```cmake
# MyProject/CMakeLists.txt
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# Source files
set(SOURCES src/main.cpp src/my_class.cpp)

# Include directories
include_directories(include)

# Add subdirectories for the main project and external library
add_subdirectory(external/MyLibrary)

# Main application target
add_executable(MyExecutable ${SOURCES})

# Link the executable with the MyLibrary target
target_link_libraries(MyExecutable PRIVATE MyLibrary)
```

```cpp
//src/main.cpp
#include <iostream>
#include "my_class.h"
#include "my_library.h"

int main() {
  MyClass myObject;
  myObject.printMessage();

  // Using MyLibrary function
  myLibraryFunction();

  return 0;
}
```

```cpp
//my_class.cpp

#include <iostream>
#include "my_class.h"

void MyClass::printMessage()
{
  std::cout << "Call MyClass::printMessage!\n";
}
```

```cpp
//include/MyLibrary/my_class.h
#pragma once

#include <iostream>

class MyClass {
public:
  void printMessage();
};
```

```cmake
# //external/MyLibrary/CMakeLists.txt
# MyLibrary target
add_library(MyLibrary
  include/my_library.h
  src/my_library.cpp
)

# Include directories for MyLibrary
target_include_directories(MyLibrary PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
```

```cpp
//external/MyLibrary/include/my_library.h
#pragma once

void myLibraryFunction();
```

```cpp
//external/MyLibrary/src/my_library.cpp
#include <iostream>
#include "my_library.h"

void myLibraryFunction() {
  std::cout << "Call myLibraryFunction!\n";
}

```

This structure demonstrates how to organize a CMake project with multiple directories. It includes a main application (`src/main.cpp`), a custom library (`include/my_class`), an external library (`external/MyLibrary`), and separate directories for build artifacts (`build`) and the final executable (`bin`). The top-level `CMakeLists.txt` file orchestrates the build process and links the main executable with the external library.
