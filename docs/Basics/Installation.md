[go back](../../README.md)

# Installation

Contents
- <a href="#installation_">Installation of GNU Compiler Collection</a>
- <a href="VSCode_Linux_Container.md">Installation via Docker (link)</a>
- <a href="#installation_via_vs">Installation via Visual Studio (Windows)</a>

<br><br>

---
<h3><a href="#top" name="installation_">Installation of GNU Compiler Collection</a></h3>

Most used compiler is the GNU Compiler Collection (GCC). It is used to compile cpp code to executable code.

<!--
- Download a C++ Compiler in **Windows**:
    - https://cygwin.com/install.html
    - make sure to install following extension (use the search bar，choose a version and click that it should get download):
        - cygwin-devel
        - gcc-g++
        - gcc-core
        - make
        - cmake
        - gdb
        - git
        - python39
        - autoconf
        - automake
        - libtool
        - ninja
        - xorg-server
        - libX11-devel
        - libXext-devel
        - libXrandr-devel
        - libXrender-devel
        - libXcursor-devel
        - libXinerama-devel
        - libXi-devel
        - libXss-devel
        - libgcc1
        - libstdc++6
    - Add cygwin to the system path variables. Then you can use the normal cmd or Powershell or the terminal in Visual Studio Code.<br>To do so，you have to search/open the system-variables (environment variables). There you search the entry "Path", there should be already some paths. To these paths you add the path of Cygwin bin folder, probably: **C:\cygwin64\bin** <br>And now it should work. Maybe a restart is requirement, if it doesn't works.
    
    - Testing (in Cygwin and or normal terminal): 
    ```terminal
    make --version
    gdb --version
    gcc --version
    g++ --version
    ```
    
> You can download additional packages by running the setup file again. It will only install the new packages.

-->
    
- Download a C++ Compiler in **Windows**:
    On windows the best option is to use MSYS2 and MinGW. MinGW provides basic mapping of linux operations to native windows operations and MSYS is a installation manager which uses MinGW to use a GCC compiler. **Do not download MinGW over the official page**, this is a old distribution and is now updated and maintained via MSYS plattform.
    - Download [MSYS2 from the official page](https://www.msys2.org/) + run the downloded installer exe and follow the instructions
    - Open the right shell.<br>
        MSYS comes with 3 shells `MSYS` (linux-like environment), `MINGW` (windows native environment), `UCRT` (modern windows native environment). For windows developement you have to use one of the last 2.<br>
        Type 
        ```bash
        echo $MSYSTEM
        ``` 
        and make sure you are in the right shell.
    - Install the GCC MinGW compiler:
        ```bash
        pacman -Syu
        pacman -S mingw-w64-ucrt-x86_64-gcc

        # or if using MINGW shell
        pacman -S mingw-w64-i686-gcc

        # or if using MSYS shell
        pacman -S gcc
        ```
    - Version checking
        ```bash
        g++ --version 
        which g++
        ```
    - Usage -> [also see](./Execution.md)
        ```cpp
        g++ main.cpp -o main.exe
        ```




- Download a C++ Compiler in **Linux**:
    - Installation: 
    ```terminal
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install make
    sudo apt-get install gdb
    sudo apt-get install gcc
    sudo apt-get install g++
    sudo apt-get install git
    sudo apt-get install cmake
    sudo apt-get install autoconf
    sudo apt-get install automake
    sudo apt-get install libtool
    sudo apt-get install ninja
    ```
    - Testing: 
    ```terminal
    gdb --version
    gcc --version
    g++ --version
    ```



<br><br>

---
<h3><a href="#top" name="installation_via_vs">Installation via Visual Studio (Windows)</a></h3>

Under Windows a very solid way to program C++ is via Visual Studio, Microsofts C++ IDE. But I do recommend to use a `CMake Project` as base project because it does not come with weird Visual Studio specific things (like that you create only virtual folders but you think they are real folders) and CMake allows an very easy and comfortable integration of external code (git repositories).

> you should have [git installed](https://git-scm.com/install/windows) on your system

1. [Download Visual Studio here](https://visualstudio.microsoft.com/de/downloads/).
2. Run the installation process and make sure to install C++ and maybe Gamedevelopement tools.
3. Next create a new project and choose "CMake Project" as base project and set the created src folder as folder and a wished name (do not place the project configure file and the project files in the same folder -> do  not check the checkbox). <br>This can be then an example structure:
    ```text
    Emerging-Light-Engine
    ----| README.md
    ----| src
    ---------| Emerging-Light-Engine
    --------------| out
    --------------| CMakeLists.txt
    --------------| CMakePresets.json
    --------------| Emerging-Light-Engine
    -------------------| Emerging-Light-Engine.cpp
    -------------------| Emerging-Light-Engine.h
    -------------------| CMakeLists.txt
    ```
    > In Visual Studio I do not see the top layer just the project in the src folder.
5. Now you can change the global CMakeLists.txt (my project name was `Emerging-Light-Engine`):
    ```cmake
    cmake_minimum_required (VERSION 3.26)
    project ("Emerging-Light-Engine" LANGUAGES CXX)

    # Activate Hot Reload for MSVC-Compiler
    if (POLICY CMP0141)
        cmake_policy(SET CMP0141 NEW)
        set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
    endif()

    set(CMAKE_CXX_STANDARD 20)

    # Schließen Sie Unterprojekte ein.
    add_subdirectory ("Emerging-Light-Engine")
    ```
6. You can also change now the sub CMakeLists.txt:
    ```cmake
    # Add 3rd Party Libraries
    include("${CMAKE_SOURCE_DIR}/Scripts/FetchLibraries.cmake")


    # Add executables (.cpp/.h)
    file(GLOB_RECURSE ENGINE_SOURCES
        "${CMAKE_SOURCE_DIR}/Emerging-Light-Engine/src/*.cpp"
    )

    file(GLOB_RECURSE ENGINE_HEADERS
        "${CMAKE_SOURCE_DIR}/Emerging-Light-Engine/include/*.h"
    )

    add_executable(Emerging-Light-Engine
        Emerging-Light-Engine.cpp
        ${ENGINE_SOURCES}
        ${ENGINE_HEADERS}
    )

    target_include_directories(Emerging-Light-Engine PRIVATE "${CMAKE_SOURCE_DIR}/Emerging-Light-Engine/include")

    # target_link_libraries(Emerging-Light-Engine PRIVATE sdl)
    target_link_libraries(Emerging-Light-Engine PRIVATE SDL3::SDL3-static)
    # target_link_libraries(Emerging-Light-Engine PRIVATE SDL3::SDL3)
    ```
7. For external code I already added `include("${CMAKE_SOURCE_DIR}/Scripts/FetchLibraries.cmake")` for downloading the external code. But for that you have to create this file. So Right-Click on the top project folder and add new folder and type `Scripts` + right-click on this new folder and add new file which you name as `FetchLibraries.cmake`
8. Inside of the new created file: -> in this case SDL but you can put whatever you want and use the version of a real release by visiting the github page and look up the release.
    ```cmake
    cmake_minimum_required (VERSION 3.26)

    include(FetchContent)

    FetchContent_Declare(
        SDL
        GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
        GIT_TAG release-3.2.28
    )

    set(SDL_SHARED OFF CACHE BOOL "" FORCE)
    set(SDL_STATIC ON CACHE BOOL "" FORCE)
    set(SDL_TEST OFF CACHE BOOL "" FORCE)

    FetchContent_MakeAvailable(SDL)
    ```
    Which will fetch SDL during building. [See here the official repo](https://github.com/libsdl-org/SDL).



