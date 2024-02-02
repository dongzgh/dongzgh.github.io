---
title: Chapter 1. Introduction to CMake
permalink: /books/cmake-by-examples/chapter-1
---

## 1.1 What is CMake?

CMake is an open-source, cross-platform family of tools designed to build, test, and package software. It provides a unified, high-level build environment for developers working on various platforms. CMake allows for the definition of the entire build process in a single, platform-independent configuration file. This file is typically named CMakeLists.txt and is used to generate native build files for different platforms and build environments, such as makefiles for Unix-based systems or project files for IDEs like Visual Studio.

CMake is particularly popular in the C and C++ development communities, as it simplifies the process of building and managing complex software projects. It abstracts the build process, enabling developers to write platform-independent CMake scripts that can generate the necessary build files for different platforms and toolchains.

Key features of CMake include its ability to manage dependencies, support for out-of-source builds, the facilitation of cross-compilation, and the generation of IDE project files. CMake also provides a range of commands and variables that allow developers to control the build process and customize the build configuration based on specific requirements. With its versatility and flexibility, CMake has become a fundamental tool for software development, helping to streamline the process of building, testing, and packaging software across various operating systems and platforms.

## 1.2 Why use CMake?

CMake offers several advantages and benefits that make it a popular choice for building and managing software projects. Some key reasons to use CMake include:

1. Cross-Platform Support: CMake allows developers to create a single build configuration that can generate native build files for various platforms, including Windows, macOS, and various Unix-like systems. This cross-platform support simplifies the process of managing and building software across different operating systems.

2. Simplified Build Process: With CMake, developers can define the build process in a high-level scripting language, making it easier to manage complex build configurations and dependencies. This simplification helps streamline the development workflow, allowing for more efficient project maintenance and updates.

3. Dependency Management: CMake facilitates the management of external dependencies and libraries, making it easier to integrate third-party components into projects. It provides mechanisms for finding and linking to external libraries, as well as tools for managing complex dependency hierarchies.

4. Integration with IDEs: CMake can generate project files for various integrated development environments (IDEs) such as Visual Studio, Xcode, and Eclipse. This feature enables developers to work within their preferred development environments while still leveraging the benefits of CMake's cross-platform capabilities.

5. Customizability: CMake offers a wide range of customization options, allowing developers to tailor the build process to specific project requirements. It provides a rich set of commands, variables, and modules that enable fine-grained control over the build configuration and compilation process.

6. Out-of-Source Builds: CMake supports out-of-source builds, which means that the build files can be generated in a separate directory from the source code. This approach keeps the source directory clean and simplifies the management of multiple build configurations.

7. Community Support and Adoption: CMake has a large and active user community, which has led to the development of extensive documentation, tutorials, and resources. This widespread adoption makes it easier for developers to find support and solutions to common issues related to project configuration and build management.

By leveraging these benefits, developers can effectively streamline the software development process, reduce build-related complexities, and ensure the seamless deployment of software across different platforms and environments.

## 1.3 How to install CMake?

The installation process for CMake can vary depending on the operating system you are using. Here are the general steps for installing CMake on different platforms:

### Installing CMake on Windows

1. **Using Installer:**
   - Visit the [CMake download page](https://CMake.org/download/) and download the Windows installer.
   - Run the installer and follow the installation instructions provided in the wizard.

2. **Using Chocolatey (Package Manager for Windows):**
   - Open a command prompt with administrator privileges.
   - Execute the following command:
  
     ```bash
     choco install CMake
     ```

### Installing CMake on macOS

1. **Using Homebrew (Package Manager for macOS):**
   - Open a terminal.
   - Run the following command:
  
     ```bash
     brew install CMake
     ```

2. **Using MacPorts (Package Manager for macOS):**
   - Open a terminal.
   - Run the following command:

     ```bash
     sudo port install CMake
     ```

### Installing CMake on Linux

1. **Using Package Manager (Ubuntu/Debian):**
   - Open a terminal.
   - Run the following command:

     ```bash
     sudo apt-get update
     sudo apt-get install CMake
     ```

2. **Using Package Manager (Fedora/CentOS):**
   - Open a terminal.
   - Run the following command:

     ```bash
     sudo dnf install CMake    # for Fedora
     sudo yum install CMake    # for CentOS
     ```

3. **Building from Source:**
   - Download the latest source code from the [CMake download page](https://CMake.org/download/).
   - Extract the downloaded archive.
   - Navigate to the extracted directory and follow the instructions in the README or INSTALL file for building and installing CMake from the source.

After installing CMake, you can verify the installation by opening a terminal or command prompt and running the following command:

```bash
CMake --version
```

This command will display the installed version of CMake and verify that it is set up correctly on your system.
