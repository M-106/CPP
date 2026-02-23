[go back](../../README.md)

# C++ Code Execution

Contents
- <a href="#compiling_and_linking">Compiling and Linking</a>
- <a href="#runcppcode">Run C++ Code with GNU</a>
- <a href="#runclangcppcode">Run C++ Code with clang++</a>
- <a href="#cmake_">CMake</a>


<br><br>

---
<h3><a name="compiling_and_linking">Compiling and Linking</a></h3>

Coming soon...

<br><br>

---
<h3><a name="runcppcode">Run C++ Code (with g++)</a></h3>

The GNU Compiler Collection (GCC) is a standard compiler for c and c++ and here you see how to use it.



Most simple way to compile a C++ program with GCC is to create a **make** file and use make to compile your C++-Files (for this you can install cygwin in Windows to use make <a href="#installation_">see here</a>):
```terminal
# Compiler
CXX = g++  # Use this if you're using MinGW or Cygwin

# Compiler flags
CXXFLAGS = -Wall -std=c++17

# List of source files
SRCS = main.cpp file1.cpp file2.cpp

# List of object files
OBJS = $(SRCS:.cpp=.o)

# Name of the output executable
TARGET = my_program.exe

# Default target: build the executable
all: $(TARGET)

# Rule to link object files into the executable
$(TARGET): $(OBJS)
    $(CXX) $(OBJS) -o $(TARGET)

# Rule to compile each source file into an object file
%.o: %.cpp
    $(CXX) $(CXXFLAGS) -c $< -o $@

# Clean up build files
clean:
    rm -f $(OBJS) $(TARGET)

```

The Makefile is just a plain textfile without a file type ending. Just name the file "Makefile" and execute it with "mingw32-make" (or "make" if not on windows).


You can also create the Makefile automatically with CMake. [See here for using CMake](#cmake_).



Another way is to type following in a terminal:
1. First you compile your program and create a executeable file:
    - ```terminal
      g++ main.cpp -o main
        ```
    - If you have multiple C++ Files you can do:
        ```terminal
        g++ -o main main.cpp game.cpp
        ```
        or:
        ```terminal
        g++ -c main.cpp
        g++ -c game.cpp
        g++ -o main main.o game.o
        ```
2. Then you can execute it:
    ```terminal
    ./main.exe
    ```
    Or in Linux:
    ```terminal
    ./main
    ```



> Hint:<br>Use the terminal and navigate with cd .. and cd 01_variables_datatypes_logic to the right folder.<br>You also can type 00 and then tab-key to use auto completion.



In Depth:
- assemble:
    ```terminal
    g++ -S program.cpp
    ```
- compile:
    ```terminal
    g++ -c program.cpp -o program.o
    ```
- build:
    ```terminal
    g++ program.o -o program
    ```


> You can add a parameter at the beginning of every command to specify how much the code should be optimized. For debugging it is common to not optimize your code to can analyze your code.<br>For Debugging: g++ -O0 -g3 ...<br>For Release: g++ -O3 ...

<br><br>

---

<h3><a name="runclangcppcode">Run C++ Code (with clang++)</a></h3>

The Clang compiler (clang/clang++) is a standard compiler for c and c++ and here you see how to use it.

Most simple way to compile a C++ program with Clang is to create a **make** file and use make to compile your C++-Files (for this you can install cygwin in Windows to use make <a href="#installation_">see here</a>):

```terminal
# Compiler
CXX = clang++  # Use this if you're using LLVM/Clang (e.g. on Linux/macOS)

# Compiler flags
CXXFLAGS = -Wall -std=c++17

# List of source files
SRCS = main.cpp file1.cpp file2.cpp

# List of object files
OBJS = $(SRCS:.cpp=.o)

# Name of the output executable
TARGET = my_program.exe

# Default target: build the executable
all: $(TARGET)

# Rule to link object files into the executable
$(TARGET): $(OBJS)
    $(CXX) $(OBJS) -o $(TARGET)

# Rule to compile each source file into an object file
%.o: %.cpp
    $(CXX) $(CXXFLAGS) -c $< -o $@

# Clean up build files
clean:
    rm -f $(OBJS) $(TARGET)

```

The Makefile is just a plain textfile without a file type ending. Just name the file "Makefile" and execute it with "make" (or "mingw32-make" if you are using it on windows).

You can also create the Makefile automatically with CMake. [See here for using CMake](#cmake_).

Another way is to type following in a terminal:

1. First you compile your program and create a executeable file:

   * ```terminal
     clang++ main.cpp -o main
     ```
   * If you have multiple C++ Files you can do:
   ```terminal
   clang++ -o main main.cpp game.cpp
   ```

   or:

   ```terminal
   clang++ -c main.cpp
   clang++ -c game.cpp
   clang++ -o main main.o game.o
   ```
2. Then you can execute it:

   ```terminal
   ./main.exe
   ```

   Or in Linux:

   ```terminal
   ./main
   ```

> Hint:<br>Use the terminal and navigate with cd .. and cd 01_variables_datatypes_logic to the right folder.<br>You also can type 00 and then tab-key to use auto completion.

In Depth:

* assemble:

  ```terminal
  clang++ -S program.cpp
  ```
* compile:

  ```terminal
  clang++ -c program.cpp -o program.o
  ```
* build:

  ```terminal
  clang++ program.o -o program
  ```

> You can add a parameter at the beginning of every command to specify how much the code should be optimized. For debugging it is common to not optimize your code to can analyze your code.<br>For Debugging: clang++ -O0 -g3 ...<br>For Release: clang++ -O3 ...



<br><br>


---
<h3><a href='#top' name='cmake_'>Using CMake</a></h3>

In bigger project it is recommended to use CMake. It generates the Makefile and than uses the Makefile to build your application.

For installation on Windows:
1. Go to https://cmake.org/download/
2. Download the windows installer
3. execute it and make sure it added to the system variables

If it got not added to the system variables:
1. Open the system variables (environment variables/Umgebungsvaribalen)
2. go to global -> 'Path'
3. add a new entry with the path to your CMake bin folder


For installation on Linux:
```terminal
sudo apt update
sudo apt install cmake
cmake --version
```


Using CMake is pretty easy. You have to create a *CMakeLists.txt* file and run it in console with:
```cmd
cd D:
cd Informatik/Projekte/CPP/src/games/01_Simple_SDL_Game
if exist build rd /s /q build
mkdir build
cd build
cmake -G "MinGW Makefiles" ..
mingw32-make 
```

And for re-running just create a run.bat file in your project folder:
```bat
:: Deactivate showing every single command
@echo off

:: Go to target path
cd /d D:\Informatik\Projekte\CPP\src\games\01_Simple_SDL_Game

:: Reset/create 'build' folder
if exist build rd /s /q build
mkdir build
cd build

:: Import external libs 
copy D:\CPPlibs\SDL\bin\SDL3.dll .

:: Create Makefile and compile C++ files
cmake -G "MinGW Makefiles" ..
mingw32-make

:: Start your Programm
start Simple_SDL_Game.exe

:: Go back to project folder
cd ..
```

And now you can easily compile your code by double click on the bat file or run the following command in the cmd in your project folder:
```cmd
run.bat
```





The CMakeLists.txt file content could look like that:
```text
cmake_minimum_required(VERSION 3.10)
# = ADJUST ME =
project(MyProject)

# Set C++ Standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add source files
# = ADJUST ME =
set(SOURCES main.cpp file1.cpp file2.cpp)

# Add executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Include External Libs -> = ADJUST ME =
# Include SDL (Custom Path)
set(SDL_DIR "/path/to/sdl")
include_directories(${SDL_DIR}/include)
link_directories(${SDL_DIR}/lib)
target_link_libraries(${PROJECT_NAME} "${SDL_DIR}/lib/libSDL3.dll.a")

# Include GLFW (Custom Path)
#set(GLFW_DIR "/path/to/glfw")
#include_directories(${GLFW_DIR}/include)
#link_directories(${GLFW_DIR}/lib)
#target_link_libraries(${PROJECT_NAME} glfw)

# Include Vulkan (Custom Path)
#set(VULKAN_DIR "/path/to/vulkan")
#include_directories(${VULKAN_DIR}/include)
#link_directories(${VULKAN_DIR}/lib)
#target_link_libraries(${PROJECT_NAME} vulkan)
```














