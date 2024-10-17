---
title: B. VS/VSCode Projects
permalink: /books/cmake-by-examples/chapter-18
---

## B.1 Visual Studio Project

To create CMake projects in Visual Studio, follow these steps:

1. **Open Visual Studio**:
   - Launch Visual Studio.

2. **Create a New Project**:
   - Go to `File` > `New` > `Project...`.

3. **Select CMake Project**:
   - In the "Create a new project" dialog, search for "CMake".
   - Select "CMake Project" from the list.
   - Click `Next`.

4. **Configure Project Details**:
   - Enter the project name and location.
   - Click `Create`.

5. **Edit CMakeLists.txt**:
   - Visual Studio will generate a basic `CMakeLists.txt` file.
   - You can edit this file to add your project configuration.

6. **Add Source Files**:
   - Add your source files (e.g., `.cpp`, `.h`) to the project directory.
   - Update `CMakeLists.txt` to include these files.

7. **Build and Run**:
   - Use the `Build` menu to build your project.
   - Use the `Debug` menu to run your project.

8. **Example project**

    ```cmake
    # CMakeLists.txt
    cmake_minimum_required(VERSION 3.5)

    project(QtBasicApp)

    set(CMAKE_CXX_STANDARD 11)

    find_package(Qt5 COMPONENTS Widgets REQUIRED)

    add_executable(QtBasicApp main.cpp)

    target_link_libraries(QtBasicApp Qt5::Widgets)
    ```

    ```cpp
    // main.cpp
    #include <QApplication>
    #include <QPushButton>

    int main(int argc, char *argv[]) {
        QApplication app(argc, argv);

        QPushButton button("Hello, Qt!");
        button.show();

        return app.exec();
    }
    ```

## B.2 Visual Studio Code Project

To create a CMake project in Visual Studio Code, follow these steps:

1. **Install Necessary Extensions**:
   - Open Visual Studio Code.
   - Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side of the window or by pressing `Ctrl+Shift+X`.
   - Install the following extensions:
     - CMake Tools
     - C/C++ (by Microsoft)

2. **Create a New Project Directory**:
   - Create a new directory for your project.
   - Open this directory in Visual Studio Code (`File` > `Open Folder...`).

3. **Create CMakeLists.txt**:
   - In the root of your project directory, create a file named `CMakeLists.txt`.
   - Add the following content to `CMakeLists.txt` for a basic Qt application:

     ```cmake
     cmake_minimum_required(VERSION 3.5)

     project(QtBasicApp)

     set(CMAKE_CXX_STANDARD 11)

     find_package(Qt5 COMPONENTS Widgets REQUIRED)

     add_executable(QtBasicApp main.cpp)

     target_link_libraries(QtBasicApp Qt5::Widgets)
     ```

4. **Add Source Files**:
   - Create a file named `main.cpp` in the same directory.
   - Add the following content to `main.cpp`:

     ```cpp
     #include <QApplication>
     #include <QPushButton>

     int main(int argc, char *argv[]) {
         QApplication app(argc, argv);

         QPushButton button("Hello, Qt!");
         button.show();

         return app.exec();
     }
     ```

5. **Configure CMake Tools**:
   - Open the Command Palette (`Ctrl+Shift+P`).
   - Type `CMake: Configure` and select it.
   - Follow the prompts to configure your project. You may need to specify the path to your CMake executable and the generator (e.g., Ninja or Unix Makefiles).

6. **Build the Project**:
   - Open the Command Palette (`Ctrl+Shift+P`).
   - Type `CMake: Build` and select it.

7. **Run the Project**:
   - Open the Command Palette (`Ctrl+Shift+P`).
   - Type `CMake: Run Without Debugging` or `CMake: Debug` to run your project.
