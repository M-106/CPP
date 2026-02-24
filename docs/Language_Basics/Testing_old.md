[go back](../../README.md)

# Testing

Testing is essential in order to make sure that your code works and this can be done automatically.

Contents
- <a href="#catch_">Testing via Catch2</a>
- <a href="#gtests_">Testing via Google Tests</a>



<br><br>

---
<h3><a name='catch_'>Testing via Catch2</a></h3>

One of the easiest and best testing methods with C++ is the [Catch 2](https://github.com/catchorg/Catch2/releases). It is super simple.

1. Go to https://github.com/catchorg/Catch2/releases/tag/v2.13.9 and download the latest .hpp file from the version **v2** (only the hpp file)
2. Add the .hpp into your project
3. Add testing code into a new test.cpp file
4. Compile your test file:
    ```
    g++ -std=c++17 tests.cpp -o tests
    ```
    Run:
    ```
    ./tests
    ```

That's it. Let's look at the tests.cpp:

```cpp
// test head
#define CATCH_CONFIG_MAIN
#include "catch.hpp"

// import code to test
// -> #include "your_file.h"
// lets define some code here for this example, but commonly you just want to include your code
int add(int a, int b) {
    return a + b;
}

int multiply(int a, int b) {
    return a * b;
}

// start testing

TEST_CASE("Addition works", "[math]") {
    REQUIRE(add(2, 3) == 5);
    REQUIRE(add(-1, 1) == 0);
    REQUIRE(add(0, 0) == 0);
}

TEST_CASE("Multiplication works", "[math]") {
    REQUIRE(multiply(2, 3) == 6);
    REQUIRE(multiply(5, 0) == 0);
    REQUIRE(multiply(-2, 3) == -6);
}

TEST_CASE("Failing test example", "[fail]") {
    REQUIRE(add(1, 1) == 2);  // This will pass
    // REQUIRE(add(1, 1) == 3);  // Uncomment to see failure

```



<br><br>

---
<h3><a name='gtests_'>Testing via Google Test</a></h3>

Another very popular C++ testing framework is GoogleTest (gtest).
It is more feature-rich than Catch2 and widely used in industry.

1. Installation can be done via cloning and building the repository by yourself or installing it on your machine (if using linux os or linux via docker).
    1. Clone it:
        ```bash
        git clone https://github.com/google/googletest.git
        ```
    2. Build and install GoogleTest
        ```bash
        cd googletest
        cmake .
        make
        sudo make install    # optional, installs to system paths
        ```
    Alternative way:
    1. Install it via apt (should install at `/usr/src/gtest`)
        ```bash
        sudo apt update
        sudo apt install libgtest-dev
        ```
    2. Maybe you have to compile it (should be at `/usr/lib/libgtest.a` and `/usr/lib/libgtest_main.a`)
        ```bash
        cd /usr/src/gtest
        sudo cmake .
        sudo make
        sudo cp lib/*.a /usr/lib
        ```
2. Create a tests.cpp, notice a similiar structure like that:
    ```txt
    project_root/
    -- src/
    --> your_code.cpp
    -- tests/
    ------> tests.cpp
    --> CMakeLists.txt
    ```
3. Write your tests 
    ```cpp
    #include <gtest/gtest.h>

    // code to test
    int add(int a, int b) {
        return a + b;
    }

    int multiply(int a, int b) {
        return a * b;
    }

    // tests

    TEST(MathTests, AdditionWorks) {
        EXPECT_EQ(add(2, 3), 5);
        EXPECT_EQ(add(-1, 1), 0);
        EXPECT_EQ(add(0, 0), 0);
    }

    TEST(MathTests, MultiplicationWorks) {
        EXPECT_EQ(multiply(2, 3), 6);
        EXPECT_EQ(multiply(5, 0), 0);
        EXPECT_EQ(multiply(-2, 3), -6);
    }

    TEST(MathTests, FailingExample) {
        EXPECT_EQ(add(1, 1), 2);
        // EXPECT_EQ(add(1, 1), 3);  // Uncomment to see a failing test
    }
    ```
4. Compile them:
    ```bash
    g++ -std=c++17 tests.cpp -lgtest -lgtest_main -pthread -o tests
    ```
5. Run tests:
    ```bash
    ./tests
    ```


Example CMAKE:
```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)

# Your source files
add_library(mycode src/your_code.cpp)

# Enable testing
enable_testing()

# Find gtest package (Ubuntu apt version)
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Tests
add_executable(run_tests tests/tests.cpp)

target_link_libraries(run_tests
    mycode
    ${GTEST_LIBRARIES}
    pthread
)

# Add to CTest
add_test(NAME runTests COMMAND run_tests)
```

This does:
- compile your code
- compile test binary
- register tests with CTest

Then run with:
```bash
mkdir build && cd build
cmake ..
make
ctest
```


