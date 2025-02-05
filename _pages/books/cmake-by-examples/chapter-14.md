---
title: Chapter 14. Testing
permalink: /books/cmake-by-examples/chapter-14
---

## 13.1 Add Google Tests

To use Google Test in CMake, you need to follow these steps:

1. **Install Google Test**: Use CMake's [`FetchContent`](command:_github.copilot.openSymbolFromReferences?%5B%22%22%2C%5B%7B%22uri%22%3A%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fdong%2FDocuments%2Fgithub%2Fresearch%2F_pages%2Fbooks%2Fcmake-by-examples%2Fchapter-13.md%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%2C%22pos%22%3A%7B%22line%22%3A21%2C%22character%22%3A10%7D%7D%5D%2C%2229d4e446-6ee3-4d9e-a8e9-b213322f293c%22%5D "Go to definition") module to download and install Google Test.
2. **Enable Testing**: Enable testing in your CMake project.
3. **Add Test Executable**: Create a test executable.
4. **Link Google Test**: Link the test executable with Google Test.
5. **Add Tests**: Register the tests with CTest.

- **Example of using Google Test**

  ```cmake
  # CMakeLists.txt
  # Minimum CMake version
  cmake_minimum_required(VERSION 3.10)

  # Project name
  project(MyProject)

  # Enable testing
  enable_testing()

  # Add GoogleTest
  include(FetchContent)
  FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/release-1.10.0.zip
  )
  # For Windows: Prevent overriding the parent project's compiler/linker settings
  set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
  FetchContent_MakeAvailable(googletest)

  # Add the main project source files
  add_executable(MyProject main.cpp)

  # Add the test executable
  add_executable(MyProjectTests test_main.cpp)

  # Link GoogleTest to the test executable
  target_link_libraries(MyProjectTests gtest_main)

  # Add tests
  add_test(NAME MyTest COMMAND MyProjectTests)
  ```

  ```cpp
  // test_main.cpp
  #include <gtest/gtest.h>

  // Example function to be tested
  int add(int a, int b) {
    return a + b;
  }

  // Test case
  TEST(AdditionTest, HandlesPositiveInput) {
    EXPECT_EQ(add(1, 2), 3);
    EXPECT_EQ(add(2, 3), 5);
  }

  int main(int argc, char **argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
  }
  ```

## 13.2 Add Custom Tests

In CMake, you can create custom tests by registering any executable or script as a test using the `add_test()` command. This is useful when you have your own custom testing framework or scripts that you want to integrate with CTest.Here are some examples of using custom tests in CMake:

- **Example 1. Custom Tests with Command-Line Arguments**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.10)
  project(CustomTestWithArguments)

  enable_testing()

  add_executable(MyApp main.cpp)

  # Add an executable for testing
  add_executable(MyArgumentTest my_argument_test.cpp)

  # Register the test with arguments
  add_test(NAME ArgumentTest COMMAND MyArgumentTest 10 20)
  ```

  ```cpp
  // my_argument_test.cpp
  #include <iostream>
  #include <cstdlib>

  int main(int argc, char* argv[]) {
    if (argc != 3) {
      std::cerr << "Usage: " << argv[0] << " <num1> <num2>\n";
      return 1;
    }

    int num1 = std::atoi(argv[1]);
    int num2 = std::atoi(argv[2]);
    int result = num1 + num2;

    if (result == 30) {
      std::cout << "Test passed!" << std::endl;
      return 0;
    } else {
      std::cerr << "Test failed: expected 30 but got " << result << std::endl;
      return 1;
    }
  }
  ```

- **Example 2. Custom Tests with Scripts**

  ```cmake
  # CMakeLists.txt (with Python script)
  cmake_minimum_required(VERSION 3.10)
  project(CustomScriptTest)

  enable_testing()

  # Register a Python script as a test
  add_test(NAME PythonTest COMMAND python3 ${CMAKE_SOURCE_DIR}/test_script.py)
  ```

  ```python
  # test_script.py
  import sys

  def test_function():
    return 1 + 1 == 2

  if __name__ == "__main__":
    if test_function():
      print("Test passed!")
      sys.exit(0)
    else:
      print("Test failed!")
      sys.exit(1)
  ```

- **Example 3. Custom Tests with Environment Variables**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.10)
  project(CustomEnvTest)

  enable_testing()

  add_executable(MyEnvTest my_env_test.cpp)

  # Register the test
  add_test(NAME EnvTest COMMAND MyEnvTest)

  # Set an environment variable for the test
  set_tests_properties(EnvTest PROPERTIES ENVIRONMENT "MY_VAR=42")
  ```

  ```cpp
  // my_env_test.cpp
  #include <iostream>
  #include <cstdlib>

  int main() {
    const char* my_var = std::getenv("MY_VAR");
    if (my_var && std::string(my_var) == "42") {
      std::cout << "Test passed: MY_VAR = " << my_var << std::endl;
      return 0;
    } else {
      std::cerr << "Test failed: MY_VAR is not set correctly" << std::endl;
      return 1;
    }
  }
  ```

- **Example 4. Custom Tests with Timeout Settings**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.10)
  project(CustomTimeoutTest)

  enable_testing()

  add_executable(MyTimeoutTest my_timeout_test.cpp)

  # Register the test
  add_test(NAME TimeoutTest COMMAND MyTimeoutTest)

  # Set a timeout for the test (e.g., 5 seconds)
  set_tests_properties(TimeoutTest PROPERTIES TIMEOUT 5)
  ```

  ```cpp
  // my_timeout_test.cpp
  #include <iostream>
  #include <thread>
  #include <chrono>

  int main() {
    std::this_thread::sleep_for(std::chrono::seconds(10));  // Sleep for 10 seconds
    std::cout << "Test completed!" << std::endl;
    return 0;
  }
  ```

- **Example 5. Adding Test Dependencies**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.10)
  project(MyProject)

  enable_testing()

  # Add the first test executable
  add_executable(MyFirstTest my_first_test.cpp)
  add_test(NAME FirstTest COMMAND MyFirstTest)

  # Add the second test executable
  add_executable(MySecondTest my_second_test.cpp)
  add_test(NAME SecondTest COMMAND MySecondTest)

  # Make SecondTest depend on FirstTest
  set_tests_properties(SecondTest PROPERTIES DEPENDS FirstTest)
  ```

  ```cpp
  // my_first_test.cpp
  #include <iostream>

  int main() {
    std::cout << "First test completed!" << std::endl;
    return 0;
  }
  ```

## 13.3. Run CMake Tests

```bash
mkdir build
cd build
cmake ..
make
ctest
```
