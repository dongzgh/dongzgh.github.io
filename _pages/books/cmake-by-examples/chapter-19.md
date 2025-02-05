---
title: C. Project Templates
permalink: /books/cmake-by-examples/chapter-19
---

## Project Template with Library and Scripts

### Directory Structure

```text
project_root/
├── CMakeLists.txt
├── src/
│   └── main.cpp
├── libs/
│   └── core/
│       ├── CMakeLists.txt
│       ├── core.h
│       └── core.cpp
└── scripts/
    └── example_script.sh
```

```cmake
# CMakeLists.txt
cmake_minimum_required(VERSION 3.14)

project(MyQtProject)

set(CMAKE_CXX_STANDARD 17)

# Find Qt libraries
find_package(Qt5 COMPONENTS Core LinguistTools REQUIRED)

# Add subdirectories
add_subdirectory(libs/core)
add_subdirectory(src)

# Translation support
file(GLOB TS_FILES "translations/*.ts")
qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
```

```cmake
# libs/core/CMakeLists.txt
add_library(core STATIC core.cpp core.h)

target_link_libraries(core Qt5::Core)
```

```cmake
# src/CMakeLists.txt
add_executable(main main.cpp)

target_link_libraries(main core Qt5::Core)
```

```cpp
// src/main.cpp
#include <QCoreApplication>
#include "core.h"

int main(int argc, char *argv[]) {
    QCoreApplication app(argc, argv);

    Core core;
    core.sayHello();

    return app.exec();
}
```

```cpp
// libs/core/core.h
#ifndef CORE_H
#define CORE_H

#include <QObject>

class Core : public QObject {
    Q_OBJECT

public:
    Core();
    void sayHello();
};

#endif // CORE_H
```

```cpp
//libs/core/core.cpp
#include "core.h"
#include <QDebug>

Core::Core() {}

void Core::sayHello() {
    qDebug() << "Hello from Core!";
}
```

```sh
# scripts/example_script.sh
#!/bin/bash
echo "This is an example script."
```

### Commands to Build and Run

```sh
mkdir build
cd build
cmake ..
make
./src/main
```
