
[go back](../../README.md)


<h1><a href='top' name='own_cpp_lib_'>Own C++ Lib</a></h1>

If you want to create your own C++ library than you are here right.

> Cloning/Downloading the source code from Github and then adding them to the search path for headers/source files of course also works.

<br><br>

---

### CMake Package

> `mapproxifold` is used as project name her as an example, replace it with your project name.

1. Make sure you export your target properly.<br>
    Add a `CMakeLists.txt` and design it similiar like the following one:

    ```cmake
    # (standard cmake the first part)

    cmake_minimum_required(VERSION 3.15)
    project(mapproxifold VERSION 1.0.0)

    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)

    # ----------------------------------------
    # Library
    # ----------------------------------------

    file(GLOB_RECURSE MAPX_SOURCES
        mapproxifold/src/*.cpp
    )

    add_library(mapproxifold ${MAPX_SOURCES})

    target_include_directories(mapproxifold
        PUBLIC
            $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/mapproxifold/include>
            $<INSTALL_INTERFACE:include>
    )

    # Give it a namespace (VERY IMPORTANT)
    add_library(mapproxifold::mapproxifold ALIAS mapproxifold)

    # ----------------------------------------
    # Install rules >>> IMPORTANT PART <<<
    # ----------------------------------------

    install(TARGETS mapproxifold
        EXPORT mapproxifoldTargets
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin
    )

    install(DIRECTORY mapproxifold/include/
        DESTINATION include
    )

    # Export target config
    install(EXPORT mapproxifoldTargets
        FILE mapproxifoldTargets.cmake
        NAMESPACE mapproxifold::
        DESTINATION lib/cmake/mapproxifold
    )

    include(CMakePackageConfigHelpers)

    write_basic_package_version_file(
        "${CMAKE_CURRENT_BINARY_DIR}/mapproxifoldConfigVersion.cmake"
        VERSION ${PROJECT_VERSION}
        COMPATIBILITY AnyNewerVersion
    )

    configure_file(
        "${CMAKE_CURRENT_SOURCE_DIR}/mapproxifoldConfig.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/mapproxifoldConfig.cmake"
        COPYONLY
    )

    install(FILES
        "${CMAKE_CURRENT_BINARY_DIR}/mapproxifoldConfig.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/mapproxifoldConfigVersion.cmake"
        DESTINATION lib/cmake/mapproxifold
    )
    ```
2. Add `mapproxifoldConfig.cmake.in` as file in your root:
    ```cmake
    include("${CMAKE_CURRENT_LIST_DIR}/mapproxifoldTargets.cmake")
    ```
3. Build + Install your library<br>You might want to open the MSYS UCTR shell (if you uses [this windows setup](../Basics/Installation.md)) and then:
    ```bash
    cd C:/project/dir/

    mkdir build
    # or
    rm -r build

    cd build
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=../install ..
    make
    make install
    ```
    Now you should have:
    ```text
    install/
    |___ include/
    │       mapproxifold/...
    |___ lib/
    │       libmapproxifold.a
    │
    |___ lib/cmake/mapproxifold/
            mapproxifoldConfig.cmake
            mapproxifoldTargets.cmake
    ```
4. Others can use your cmake package with adding this into their cmake files:
    ```cmake
    cmake_minimum_required(VERSION 3.15)
    project(my_app)

    find_package(mapproxifold REQUIRED)

    add_executable(my_app main.cpp)

    target_link_libraries(my_app PRIVATE mapproxifold::mapproxifold)
    ```
    Then they can install it:
    ```
    cmake -DCMAKE_PREFIX_PATH="path/to/install" ..
    ```

<br><br>

---

### With Visual Studio

1. Make a git project in github and make sure to click "Make README.md" + you can also directly add a License.md
2. Clone your repository to your local system
3. Open Visual Studio and create a new *Dynamische Bibliothek (DLL)* or *Statische Bibliothek (LIB)* -> dynamic if you have many external libraries else static should be fine + make sure to create the solution file outside of the project folder (uncheck the box) + the location should be the folder, where your git project was created/cloned to and the name should be same from the git and vs
4. create a *tensor-rush.hpp* with -> same name as your project:
    ```cpp
    #pragma once


    #ifdef TENSOR_RUSH_EXPORTS
    #define TENSOR_RUSH_API __declspec(dllexport)
    #else
    #define TENSOR_RUSH_API __declspec(dllimport)
    #endif


    class TENSOR_RUSH_API MeineKlasse {
    public:
        MeineKlasse();
        void sagHallo();
    };
        ```
    5. create a *tensor-rush.cpp* with -> same name as your project:
        ```cpp
    #include "pch.h"
    #include "tensor-rush.hpp"

    #include <iostream>

    MeineKlasse::MeineKlasse() {}

    void MeineKlasse::sagHallo() {
        std::cout << "Hallo von der Bibliothek!" << std::endl;
    }
    ```
6. You also have to add the Export key, so go to ```right-click on the lib project > properties > C/C++ > Preprocessor > Preprocessordefinitions``` and add there *TENSOR_RUSH_EXPORTS*
7. With ```right-click on the project > build```, you can *build* it, which will create the .dll and .lib files 
8. Testing/running your lib
    1. Create a local test project inside of your top project by ```right-click on the project name > add > new project```  just named "test" and a normal empty C++ project. 
    2. You have to ```right-click on the test project > properties > C/C++ > General > Additional Include Directories``` and add the path to the folder, where the .hpp/.h files are.  
    3. You have to ```right-click on the test project > properties > Linker > General > Additional Librarydirectories``` and add the path to the folder, where the .dll and .lib files are.
    4. You have to ```right-click on the test project > properties > Linker > Input > Additional Dependencies``` and add all .lib names (here for example tensor-rush.lib)
    5. Now  you can try to use your lib.  Main.cpp:
        ```cpp
        #include <iostream>
        #include "meine_lib.hpp"

        int main() {
            MeineKlasse obj;
            obj.sagHallo();
            return 0;
        }
        ```
    6. To run the test, you have to click the small arrow next to the green running arrow button and choose *startproject configure* and choose there that the test should run if the button is clicked.
9. You can share your .h, .dll and .lib, so that other can use your library.


> Executable files and .lib / .dll files should be added not directly in your git repo, else it should be added in releases, because you don't want to track the executable and lib files.<br>You may want to create a release folder witht the right


It is often recommended to create a folder structure, so that your code is well structured. In Visual Studio you can do that as virtual, so the real files are in all the same place and the project solution file saves which file is in which virtual folder. Example substructure:
```
tensor-rush/
│── include/                  # header files
│   ├── tensor-rush.h         # main header
│   ├── core/
│   │   ├── log.h             # Logging-Functions
│   │   ├── math.h            # Math-Functions
│   ├── utils/
│   │   ├── file_io.h         # File Operations
│   │   ├── string_utils.h    # String-Utilities
│
│── src/                      # cpp files
│   ├── tensor-rush.cpp       # main implementation
│   ├── core/
│   │   ├── log.cpp
│   │   ├── math.cpp
│   ├── utils/
│   │   ├── file_io.cpp
│   │   ├── string_utils.cpp
│
│── lib/                      # external dll or lib files
│   ├── Vulkan.lib            
│   ├── OpenGL32.lib
│
│── tests/                    # Unit-Tests
│   ├── main_test.cpp
```

The tensor-rush.hpp is now the master headerfile, which includes every other available header file, so the user have to include only the tensor-rush.hpp.


Congratulations!!! You should be able now to make your own lib! 😇


