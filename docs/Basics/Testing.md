[go back](../../README.md)

# Testing

Testing is a key component of stable software performance and make changes reliable. There is even a common programming procedure known as test-driven-developement (TDM) with following procedure:
1. Write tests of the new functionality
2. Let the tests fail (run them)
3. Implement the feature
4. Let the tests succeed (change the implementation until it succeed in the tests)

While there are different tests, most easy and common are the **Unit-Tests** where every base functionality (unit) is tested by its own. This brief guide only focuses on these tests.<br>
Tests have also criteria and should be programmed carefully, a failing test might just mean tht the test itself is wrong.
Some Criteria are:
- One Test should only test one functionality only (makes debugging and implementing more easy)
- All cases should be covered

Tests can be done via many libraries. We introduce testing with the catch2 library.

<br><br>

---

### Installation

Installing Catch2 via MSYS is pretty easy:<br>
Open your MSYS UCTR shell and install it:
```
pacman -S mingw-w64-ucrt-x86_64-catch
# or when using MSYS MinGW
pacman -S mingw-w64-x86_64-catch2
```

> For base C++ setup see the [installation guide](./Installation.md).


<br><br>

---

### Writing Tests

Writing tests, just add `.cpp` files in a `tests` folder and make them like this:

```bash
#include <catch2/catch_test_macros.hpp>
#include <mapproxifold/neural_network.hpp>

TEST_CASE("Neural network constructs correctly")
{
    mapproxifold::neural_network net;
    REQUIRE(true);  // placeholder test
}

TEST_CASE("Basic math works")
{
    REQUIRE(2 + 2 == 4);
}
```

<br><br>

---

### Run Tests

Common way it to use CMake and add there there the tests. Here is an example for a project named mapproxifold.
Add the CMake file as `CMakeLists.txt`.

```cmake
cmake_minimum_required(VERSION 3.15)
project(mapproxifold)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# --------------------------------------------------
# Library
# --------------------------------------------------

file(GLOB_RECURSE MAPX_SOURCES
    mapproxifold/src/*.cpp
)

add_library(mapproxifold ${MAPX_SOURCES})

target_include_directories(mapproxifold PUBLIC
    ${PROJECT_SOURCE_DIR}/mapproxifold/include
)

# Optional: warnings (recommended)
target_compile_options(mapproxifold PRIVATE
    $<$<CONFIG:Debug>:-g>
    $<$<CONFIG:Release>:-O3>
)

# --------------------------------------------------
# Catch2
# --------------------------------------------------

find_package(Catch2 3 REQUIRED)

# --------------------------------------------------
# Test executable
# --------------------------------------------------

add_executable(test_app
    tests/test.cpp
)

target_link_libraries(test_app PRIVATE
    mapproxifold
    Catch2::Catch2WithMain
)

# --------------------------------------------------
# Enable testing
# --------------------------------------------------

include(CTest)
include(Catch)

catch_discover_tests(test_app)
```

Then run with:
```bash
mkdir build-debug
# or
rm -r build-debug

cd build-debug

cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Debug ..

ninja

# without ninja:
# cmake -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Debug ..
# make

ctest
```


> `ctest` only runs the catch tests if you added `include(Catch)` and `catch_discover_tests(test_app)` in your cmake file as shown before.


