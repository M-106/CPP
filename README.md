<h1><a name="top">C++ Reference</a></h1>

This project contains knowledge about the C++ language.
An amazing programming langauge which is most likely preferred for software developement, rendering/graphical applications and compute intense applications. Through the long history and the near to the C language there are some legacy ways to use C++ and modern ways to use C++.<br>
I always found that C++ code is much prettier and more logical and gives the programmer more structure to hold on compared to other programming languages but of course you pay with flexibility compared to languages like python or julia.<br>
This is project tries to catch the basics of (modern) C++ as well as some most interesting parts, like game programming, graphics rendering and general GPU calculations.

May use it as a reference ❤️


### Content:

- **Basics** (Installation & Execution)
    - <a href="./docs/Basics/Installation.md">Installation</a>
    - <a href="./docs/Basics/Execution.md">Code Execution</a>
    - <a href="./docs/Basics/Testing.md">Testing</a>
    - <a href="./docs/Basics/Environment.md">Coding Environment</a>
    - <a href="./docs/Basics/Introduction.md">Introduction</a>
- **Language Basics**
    - <a href="#basics_">Quickreference</a>
    - <a href="./docs/Language_Basics/Own_Lib.md">Own C++ Library</a>
    - <a href="./docs/Language_Basics/Testing.md">Testing</a>
- **Standard Library**
    - ...
- **External Libraries**
    - Rendering and Accelaration Usage
        - <a href="./docs/External_Libraries/Rendering/OpenGL.md">OpenGL</a>
        - <a href="./docs/External_Libraries/Rendering/Vulkan.md">Vulkan</a>
        - <a href="./docs/External_Libraries/Rendering/Vulkan_Compute.md">Vulkan Compute</a>
- **Additional Topics**
    - <a href="./docs/Additional_Topics/Game.md">Gaming</a>
    - <a href="./docs/Additional_Topics/CPP_to_Python.md">C++ to Python</a>
- **Example projects**
    - [3D C++ Game-Engine: Emerging-Light-Engine](https://github.com/M-106/Emerging-Light-Engine) 





<br><br>

<!-- <img src="./cover.jpeg"></img> -->






---
<h3><a href="#top" name="basics_">Quickreference</a></h3>

This part contains the most essential knowledge about C++ shorten for a lunch break.

<a name="bascis_top_">Contents:</a>
- <a href="#basics_compiling_cpp">Compiling</a>
- <a href="#basics_header_cpp">Header and C++ Files</a>
- <a href="#basics_stack_and_heap_">Stack and Heap</a>
- <a href="#basics_main_">Main</a>
- <a href="#basics_datatypes_">Datatypes</a>
- <a href="#basics_char_and_strings_">Chars and Strings</a>
- <a href="#basics_optional_">Optional</a>
- <a href="#basics_flow_structures_">Flow Structures</a>
- <a href="#basics_value_categories_">Value Categories</a>
- <a href="#basics_variable modifier_">Variable Modifiers</a>
- <a href="#basics_pointers_">Pointers</a>
- <a href="#basics_smart_pointers_">Smart Pointers</a>
- <a href="#basics_references_">References</a>
- <a href="#basics_arrays_">Arrays</a>
- <a href="#basics_collections_">Collections</a>
- <a href="#basics_templates_">Templates</a>
- <a href="#basics_namespaces_">Namespaces and Headerfiles</a>
- <a href="#basics_std_">Standard Library</a>
- <a href="#basics_classes_">Classes</a>
- <a href="#basics_structs_">Structs</a>
- <a href="#basics_class_methods">Class Methods</a>
- <a href="#basics_brace_init_">Brace Initialization</a>
- <a href="#basics_move_semantics_">Move Semantics</a>
- <a href="#basics_error_handling_">Error Handling</a>
- <a href="#basics_cpp_paradigms_">Programming Paradigms</a>.
- <a href="#basics_best_practices_">Best Practices</a>
- <a href="#basics_modern_cpp_">Modern C++</a>
- <a href="#basics_examples_">Examples</a>
- <a href="#basics_common_errors_">Common Errors</a>




It follows some keyconcepts to keep in mind when working with C++.

<br><br>

<a name="basics_compiling_cpp" href="#bascis_top_">^</a><br>
**Compiling**

C++ does not come with its own auto Compiling tool. The user have to use an compiler by himself.

Most likely you can use an compiler directly or use an tool for more features, like `CMake`.

The compiling process goes through every explicitly given `.cpp`-file and runs:
1. **Preprocessor**
    - **Include Header files**<br>
        Paste the *declaration* (and definitions) from included header files inside the code (if using macros like `#pragma once` or `#ifndef #define ... #endif` the code gets only pasted if not pasted already earlier).
    - **Process Macros**
2. **Compiler**
    - **Convert to `.obj`**<br>
        Creates object code, which is machine code (binary) with missing references/jumps which will be added at the next step.
3. **Linker**
    - **Links object files + external files**<br>
        The different `.obj`-files gets linked to each other and merged also with external files to one executable machine code.

<br><br>

Available C++ compiler:
- GCC (g++) – Very common on Linux and Windows (via MinGW)
- Clang (clang++) – Modern, fast, great diagnostics
- MSVC (cl.exe) – Microsoft Visual C++ compiler on Windows
- Intel oneAPI (icpx / icc) – Optimized for Intel CPUs

<br><br>

Running C++ compiler:

With GCC:
- Compile a single file:
    ```bash
    g++ main.cpp -o program
    ```
- Compile multiple files:
    ```bash
    g++ main.cpp utils.cpp math.cpp -o program
    ```
- Specify C++ standard:
    ```bash
    g++ -std=c++20 main.cpp -o program
    ```
- Add include directory (where it searches for `.h`/`.hpp` files):
    ```bash
    g++ -Iinclude main.cpp -o program
    ```
- Create object files manually:
    ```bash
    g++ -c main.cpp
    g++ -c utils.cpp
    g++ main.o utils.o -o program
    ```

With clang:
- Compile a single file:
    ```bash
    clang++ main.cpp -o program
    ```
- Compile multiple files:
    ```bash
    clang++ main.cpp utils.cpp math.cpp -o program
    ```
- Specify C++ standard:
    ```bash
    clang++ -std=c++20 main.cpp -o program
    ```
- Add include directory (where it searches for `.h`/`.hpp` files):
    ```bash
    clang++ -Iinclude main.cpp -o program
    ```
- Create object files manually:
    ```bash
    clang++ -c main.cpp
    clang++ -c utils.cpp
    clang++ main.o utils.o -o program
    ```

<br><br>

Using CMake for C++ compiling:

CMake generates platform-specific build files (Makefiles, Ninja, Visual Studio projects, etc.).

Minimal project structure:
```text
project/
 ├─ CMakeLists.txt
 └─ src/
     └─ main.cpp
```

Minimal `CMakeLists.txt`:
```txt
cmake_minimum_required(VERSION 3.16)
project(MyProgram)

set(CMAKE_CXX_STANDARD 20)

add_executable(MyProgram src/main.cpp)
```

Build with CMake:
```bash
mkdir build
cd build
cmake ..
cmake --build .
```

Run program:
```bash
./MyProgram
```




<br><br>

<a name="basics_header_cpp" href="#bascis_top_">^</a><br>
**Header Files and C++ Files**

In modern C++, projects are typically divided into header files (.h / .hpp) and implementation files (.cpp).<br>
This separation improves readability, reusability, and compile times.<br>
But there some exceptions, where a header file also includes the implementation directly.

<br><br>

**Header Files (`.h` / `.hpp`)**

Header files contain declarations - not implementations.

They usually include:
- Class and struct definitions
- Function declarations (signatures)
- Constants, enums, type aliases
- Inline or template function definitions (when required)

Example:
```c++
// MathUtils.hpp

#ifndef MATHUTILS_HPP
#define MATHUTILS_HPP
#include <vector>

class MathUtils {
public:
	static double mean(const std::vector<double>& values);
};

#endif
```

During the prepare step the code from the header files will be added to the places where `#include "my_awesome.h"` calls them. To make sure that your definitions only get imported once (duplicated definitions are not allowed) you have to add code to make sure that your code only processes once.

A modern but not standard way is one line in the .h file `#pragma once` but some compiler may process this differently. Therfeore the standard method is recommended:
```c++
#ifndef MY_FILE_NAME_H
#define MY_FILE_NAME_H

// ...

#endif
```

The macro definition which you do with these 3 lines is not connected to your actual file and just is a definition name. So do not think too much about this definition name. A good convention is to name it like the file but everything uppercase and special tokens like `.` and `-` have get changed to `_`.

Not standard way:
```c++
#pragma once

// ...
```

<br><br>

**Implementation Files (`.cpp`)**

Implementation files contain the definitions (bodies) of declared functions and methods.

```c++
// MathUtils.cpp
#include "MathUtils.hpp"
#include <numeric>

double MathUtils::mean(const std::vector<double>& values) {
	if (values.empty()) return 0.0;
	double sum = std::accumulate(values.begin(), values.end(), 0.0);
	return sum / values.size();
}
```


<br><br>

<a name="basics_stack_and_heap_" href="#bascis_top_">^</a><br>
**Stack and Heap**<br>
In C++ there are 2 main storage types which should be known. One is the stack, a small memory where all local variables/values get stacked. The stack defines variables/values just in a local area, called scope. For example a function call creates a new scope on the stack and the variables are only avaiable on this scope. If the function call finsihes than the scope closes and the memory of these variables get free again.<br>
The heap is the other storage type, it provides much more storage capacities and have no scopes (there is no stacking). But the variables and values here does not delete themselfs, so the programmer have to delete the values here if they are not used anymore. Else a memory leak occur, where the taken memory accumulates and on some point the heap overflows and the program crashes.<br>
The heap always need pointer to its values and the programmer can decide which objects to createw where. Int values for example can be created in the stack or in the heap. The 'new' key shows when something is created in the heap and the 'delete' / 'delete[]' is for releasing/freeing memory.<br>
More about how to create variables where comes in a next chapter.<br>
'Dynamic allocation' refers to variables which lay in the heap because they are dynamic managed in the heap by the programmer and not bound to the scope/program flow. 'Static allocation' (or automatic allocation) refers to variables which are created in the stack. They are static because they are bound to it's scope/program flow.


<br><br>

<a name="basics_main_" href="#bascis_top_">^</a><br>
**Main**<br>

Every C++ program start with a `main` function. This function have to return the exit state of the program (`0` in normal case) and it comes in 2 forms:
```cpp
int main();
int main(int argc, char *argv[]);
```

One without commandline arguments and another with.

In `int main(int argc, char *argv[])` `argc` defines the amount of passed arguments and *argv[] is an c-style array of the arguments (c-style arrays are always a pointer to the first element). The argument range is from `argv[0]` (if there is more than 0 elements) to `argv[argc-1]`.




<br><br>

<a name="basics_datatypes_" href="#bascis_top_">^</a><br>
**Datatypes**<br>
Basic Data Types
- bool → Boolean (true or false)
- char → Character (1 byte)
- int → Integer (4 bytes, platform-dependent)
- float → Floating-point number (4 bytes)
- double → Double-precision floating-point number (8 bytes)
- void → Represents "no type" (used for functions with no return value)

Integer Variants
- short → Short integer (2 bytes)
- long → Long integer (at least 4 bytes)
- long long → Longer integer (at least 8 bytes)
- unsigned → Unsigned version (positive numbers only)

Floating-Point Variants
- long double → Extended-precision floating-point number

Derived Data Types
- pointer → Stores memory addresses (int*, char*, etc.)
- reference → Alias to another variable (int&)
- array → Collection of elements of the same type (int arr[10];)
- function → Defined return type and parameters (int func(int x);)

User-Defined Data Types
- struct → Custom data structure
- class → Object-oriented data structure
- union → Memory-sharing structure
- enum → Enumeration of constant values
- typedef / using → Define custom type aliases

(Standard Library Types -> STD)<br>
STD Integer-Types (with fixed bit width over all OS)
- std::int8_t → 8-bit signed integer
- std::uint8_t → 8-bit unsigned integer
- std::int16_t → 16-bit signed integer
- std::uint16_t → 16-bit unsigned integer
- std::int32_t → 32-bit signed integer
- std::uint32_t → 32-bit unsigned integer
- std::int64_t → 64-bit signed integer
- std::uint64_t → 64-bit unsigned integer

STD Helper-Types
- std::size_t → Unsigned integer for memory sizes (e.g. sizeof(), array indices)
- std::ptrdiff_t → Signed integer, difference between two pointers
- std::nullptr_t → Type for nullptr

STD Character-Types
- std::byte → Raw data byte (from C++17, no direct numeric type)
- std::char_traits<char> → Character handling (used internally by std::string)
- std::wchar_t → Wide character type for Unicode
- std::char16_t, std::char32_t → Unicode types for UTF-16/UTF-32

STD Container-Types
- std::string → Dynamic string
- std::vector<T> → Dynamic array
- std::array<T, N> → Fixed size static array
- std::list<T> → Double linked list
- std::map<K, V> → Associative array (key-value pairs)
- std::unordered_map<K, V> → Hashmap for quick access
- std::set<T> → Set with unique elements
- std::queue<T> → FIFO queue

STD SmartPointers-Types
- std::unique_ptr<T> → Unique ownership (no delete necessary)
- std::shared_ptr<T> → Shared ownership with reference counting
- std::weak_ptr<T> → Weak pointer (prevents cycle problems)

STD Threading-Types
- std::thread → Start threads
- std::mutex → Locks resources to threads
- std::atomic<T> → Thread-safe atomic operations


<br><br>

<a name="basics_char_and_strings_" href="#bascis_top_">^</a><br>
**Chars and Strings**

For me, who came from Python, `chars` where a bit confusing for me at first. So let's wrap this topic up a bit.

**Chars** - single character

```cpp
char c = 'A';    // single character
```

Rules:
- Must use single quotes `'A'`
- Holds a single byte (typically ASCII)
- Cannot store `"Hello"` → that's a string
- Can do arithmetic on char (like `'A'` + 1 → `'B'`)

There are also chars for Unicode:
| Type       | Literal | Size               | Notes     |
| ---------- | ------- | ------------------ | --------- |
| `char16_t` | `u'A'`  | 16-bit             | UTF-16    |
| `char32_t` | `U'A'`  | 32-bit             | UTF-32    |
| `wchar_t`  | `L'A'`  | platform-dependent | wide char |

```cpp
char16_t c16 = u'Ω';
char32_t c32 = U'🌟';
```


<br><br>

**String literals** - multi character array

```cpp
const char* hello = "Hello";
```

Rules:
- Must use double quotes "Hello"
- Type: const char* (pointer to first character in array)
- Immutable (cannot change content safely)
- Null-terminated ('\0' at the end)

So be careful with that datatype and most likely use the real string from std instead, else this can happen:

```cpp
hello[0] = 'h'; // undefined behavior, "not allowed"
```

<br><br>

**`std::string`** - real C++ String

```cpp
#include <string>

std::string s = "Hello";
s += " World";        // concatenate
std::cout << s[0];    // access first char: 'H'
```

Features:
- Dynamic size
- Can be concatenated (+ or +=)
- Can convert from const char* automatically


String construction:
```cpp
std::string name = "Alice";  // is ok, but in some cases can be also interpretated as String literal, so be careful
std::string name2 = std::string("Alice");  // explicit
```

String methods:
| Operation   | Example                 |
| ----------- | ----------------------- |
| size        | `s.size()`              |
| empty       | `s.empty()`             |
| concatenate | `s1 + s2` or `s1 += s2` |
| access      | `s[i]`, `s.at(i)`       |
| substring   | `s.substr(1, 3)`        |
| find        | `s.find("llo")`         |
| erase       | `s.erase(1, 3)`         |
| insert      | `s.insert(0, "Hi")`     |


Converting string to char:
```cpp
char c = 'A';
std::string s(1, c);   // convert char → string "A"

std::string str = "B";
char c2 = str[0];      // first char
```

Other helpful functions come with `#include <string>`

| Function / Feature                                                                 | Header                                        | Notes                                            |
| ---------------------------------------------------------------------------------- | --------------------------------------------- | ------------------------------------------------ |
| `std::string`                                                                      | `<string>`                                    | The main C++ string class                        |
| `std::to_string(int/double/...)`                                                   | `<string>`                                    | Convert numbers to strings                       |
| `std::stoi`, `std::stol`, `std::stod`, etc                                         | `<string>`                                    | Convert string → number                          |
| `std::getline`                                                                     | `<string>` (with `<istream>` or `<iostream>`) | Read a line from stream into a string            |
| `std::ostringstream` / `std::stringstream`                                         | `<sstream>`                                   | Build strings by streaming data                  |
| String member functions like `size()`, `substr()`, `find()`, `insert()`, `erase()` | `<string>`                                    | Standard string operations                       |


<br><br>

**String Streams** - buffered Strings

(special case, most likely no need for it)

`std::stringstream` is a standard C++ stream that writes to a string instead of a file or console.<br>
Think of it as a buffer where you can “stream” text and numbers, then get the final string at the end.

Usage:
```cpp
#include <sstream>
#include <string>
#include <iostream>

int main() {
    std::stringstream ss;

    std::string name = "Alice";
    int age = 30;

    // stream like you would to std::cout
    ss << "Name: " << name << ", Age: " << age;

    // convert to string
    std::string result = ss.str();

    std::cout << result << std::endl;
}
```

Append numbers and strings:
```cpp
int x = 10;
double y = 3.14;
std::stringstream ss;

ss << "x=" << x << ", y=" << y;

std::string out = ss.str();  // "x=10, y=3.14"
```

Reset the stream:
```cpp
ss.str("");       // reset content
ss.clear();       // reset error flags
ss << "Hello";    // reuse
```

Build complex messages (logging):
```cpp
std::stringstream log;
log << "Controller " << cid << " pressed button " << button;
std::string message = log.str();
std::cout << message << std::endl;
```

Bonus: you can add such an streaming operation to your own class, see this example:

```cpp
#include <iostream>
#include <string>

class MyClass {
    std::string name;
    int value;

public:
    MyClass(std::string n, int v) : name(n), value(v) {}

    // declare friend operator
    friend std::ostream& operator<<(std::ostream& os, const MyClass& obj);
};

// define operator
std::ostream& operator<<(std::ostream& os, const MyClass& obj) {
    os << "Name: " << obj.name << ", Value: " << obj.value;
    return os;  // must return os to allow chaining
}

int main() {
    MyClass obj("Alice", 42);
    std::cout << obj << std::endl;
}
```

<br><br>
(Last) Bonus:

F-string style formatting:
```cpp
#include <iostream>
#include <format>

int my_int = 12;
std::cout << std::format("My favourite number is {}. I really love it.", my_int) << std::endl;
```


<br><br>

<a name="basics_optional_" href="#bascis_top_">^</a><br>
**Optional**<br>

- **Header:** `<optional>`
- **Namespace:** std
- **C++ Standard:** C++17+

Definition:<br>
`std::optional<T>` is a type that may or may not contain a value of type T. It is a safer, modern alternative to using raw pointers or sentinel values like -1 or nullptr to represent "no value".

```cpp
#include <optional>
#include <string>

std::optional<int> maybe_number;        // empty optional
std::optional<std::string> maybe_name;  // empty optional
```
- Default-constructed optional is empty (`nullopt`)
- Can hold any copyable or movable type

<br><br>

Assigning to values:
```cpp
maybe_number = 42;            // optional now holds 42
maybe_name = "Alice";         // optional holds a string
maybe_number = std::nullopt;  // make it empty again
```

- `std::nullopt` is a constant representing "no value"
- `.reset()` is equivalent to assigning `std::nullopt`

```cpp
maybe_number.reset();  // clears the value
```

<br><br>

Check for a value:
```cpp
if (maybe_number.has_value()) {
    std::cout << "Value: " << maybe_number.value() << "\n";
}

if (maybe_name) {  // implicit conversion to bool
    std::cout << "Name: " << *maybe_name << "\n";
}

if (maybe_number == std::nullopt) {
    std::cout << "No value\n";
}
```

- `.has_value()` returns `true` if optional contains a value
- `*opt` or `opt.value()` accesses the contained value
- `opt.value()` throws `std::bad_optional_access` if empty

<br><br>

Accessing values safely:
- Default fallback value:
    ```cpp
    int n = maybe_number.value_or(0);  // 0 if empty
    std::string s = maybe_name.value_or("Unknown");
    ```
- Conditional access:
    ```cpp
    if (maybe_number) {
        int val = *maybe_number;  // use value
        // or
        // int val = maybe_number.value();
    } else {
        // handle empty case
    }
    ```

<br><br>

Examle usage in a function (often used in functions as parameters for optional arguments):

```cpp
#include <optional>

void update_button(bool pressed, std::optional<DpadState> dpad = std::nullopt) {
    if (dpad) {
        current_dpad = *dpad;
    }
}
```

<br><br>

Summary:

| Function             | Description                                       |
| -------------------- | ------------------------------------------------- |
| `.has_value()`       | Returns true if optional contains a value         |
| `.value()`           | Returns the value (throws if empty)               |
| `*opt`               | Dereference to get value                          |
| `.value_or(default)` | Get value or fallback if empty                    |
| `.reset()`           | Remove contained value, makes optional empty      |
| `operator bool()`    | Implicit conversion to `true` if contains a value |


<br><br>

<a name="basics_flow_structures_" href="#bascis_top_">^</a><br>
**Flow Structures**<br>
Conditional Statements
- if → Executes a block if a condition is true
- if-else → Executes one block if true, another if false
- else if → Multiple conditions in sequence
- switch-case → Multi-way branching based on a single value
- ?: (Ternary Operator) → Short inline conditional

Loops
- for → Loop with an initializer, condition, and increment
- while → Loop that runs while a condition is true
- do-while → Like while, but runs at least once

Jump Statements
- break → Exits a loop or switch statement
- continue → Skips to the next loop iteration
- return → Exits from a function
- goto → Jumps to a labeled statement (rarely used)

Exception Handling
- try → Defines a block of code to test for exceptions
- catch → Handles exceptions thrown by throw
- throw → Throws an exception

Others
- Range-based for (for (auto x : collection))
- Lambda expressions (used for inline logic)
- Coroutines (co_await, co_yield, co_return in C++20)

<br><br>

<a name="basics_value_categories_" href="#bascis_top_">^</a><br>
**Value Categories**<br>
Lvalues are values which are stored/connected with a variable.<br>
Values which are just passed by as a parameter and therfore have no memory location are called rvalues.<br>
Glvalues (Generalized Lvalues) are all values which have an address.<br>
Xvalues are expriting values which are about to destroy.<br>
And Prvalues which are rvalues which have a memory address.

<br><br>

<a name="basics_variable modifier_" href="#bascis_top_">^</a><br>
**Variable Modifier**<br>
Variables can be 'const' -> constant, means the value is not allowed to change. This is 
const (Constant Variable)

- const
	- The value cannot be changed after initialization.
	- Used for defining constants and preventing modifications to function parameters.
	- Helps avoid unintended side effects.
	- Efficient for references since they don’t require additional memory allocation.
	- Useful for constants which value never should get changed in the program or for function parameters, to make sure that the passed reference is not changed and does so not lead to unwanted sideeffects -> why we want unchangable references? because references are most lowest at resource consuming.

- volatile
    - Tells the compiler that the variable can be changed at any time (e.g., by hardware or another thread).
    - Prevents compiler optimizations that assume the value won’t change unexpectedly.

- mutable
	- Allows modification of a variable inside a const object.
    - Typically used with const class methods to modify specific members.

- static
    - Inside a function: Retains its value across function calls.
    - Inside a class: Shared among all instances (i.e., belongs to the class, not an object).
    At global scope: Limits visibility to the current translation unit (file).

- extern
    - Declares a global variable defined in another file or translation unit.
    - Used for sharing variables across multiple files.

- register (Deprecated)
    - Suggested storing the variable in a CPU register for fast access.
    - Modern compilers optimize this automatically, making it obsolete.

- thread_local
    - Creates a variable that is unique to each thread.
    - Useful for thread-safe programming without explicit locking.

<br><br>

<a name="basics_pointers_" href="#bascis_top_">^</a><br>
**Pointers**

> The first part is about legacy pointers, which can be interesting to know, but please **use the smartpointers, which are described in <a href="#basics_smart_pointers_">the next chapter</a>**.

Pointers are variables pointing to another memory address. A pointer have a own memory adress and the value saved is the memory address where the pointer points to.<br>
Pointer are important to use the heap efficiently.<br>
Pointer are declared with a \* and need to get a memory address, which can be provided with a & before the target variable.
```c++
int i = 36;
int* pointer_i = &i;
```

- \*pointer_name -> returnes the value of the pointed address.
- &pointer_name -> returns the memory address of the pointer
- pointer_name -> returns the memory address where it points to
```c++
int* p = new int{12};
*p = 8;    // *pointer_name returnes the value of the pointed address
&p;    // &pointer_name returns the memory address of the pointer
p;   // pointer_name returns the memory address where it points to
```

Pointers can also point to nothing:
```c++
#include <iostream>
#include <cstdint>

template <typename T>
// reference on a pointer is needed to get the real memory address and don't create a new pointer
void print_pointer(T*& pointer_i){
	if(pointer_i != nullptr){
		std::cout << "Your pointer points to " << pointer_i;
	    std::cout << " with the value -> " << *pointer_i;
	    std::cout << " pointer memory asdress -> " << &pointer_i;
	    std::cout << std::endl;
	} else {
		std::cout << "Your pointer points to nothing!";
		std::cout << " pointer memory asdress -> " << &pointer_i;
		std::cout << std::endl;
	}
}

int main() {
	int* pointer_i = nullptr;
	auto* pointer_i2 = new std::int32_t{20};
	
	print_pointer(pointer_i);
	print_pointer(pointer_i2);
	
	delete pointer_i;
	delete pointer_i2;
}
```
Important: 'const' makes not the pointer constant but it's value address.

> Do not use such pointers in modern code!!! Use smartpointers instead.


<br><br>

<a name="basics_smart_pointers_" href="#bascis_top_">^</a><br>
**Smart Pointer**

Smart pointers are **RAII (Resource Acquisition Is Initialization)** objects that automatically manage memory.
They are defined in `<memory>` and replace raw pointers (`new` / `delete`) in modern C++.

Smart pointers ensure that dynamically allocated memory is **automatically released** when the pointer goes out of scope - avoiding memory leaks and dangling pointers.

Use:<br>
`std::make_unique<T>()` and `std::make_shared<T>()`

<br><br>

**std::unique_ptr**

Owns a resource exclusively. Only one unique_ptr can manage a given object at a time.

```c++
#include <memory>
#include <iostream>

struct Entity {
	Entity(int id) : id(id) { std::cout << "Created " << id << '\n'; }
	~Entity() { std::cout << "Destroyed " << id << '\n'; }
	int id;
};

int main() {
    // std::unique_pointer<Entity> e = std::make_unique<Entity>(42);
    // std::unique_pointer<Entity> e(Entity(42));
	auto e = std::make_unique<Entity>(42);
	std::cout << e->id << '\n';

	// Ownership transfer
	auto e2 = std::move(e);   // e is now nullptr
	if (!e) std::cout << "e no longer owns the Entity\n";
}
```

> Do not copy a `unique_ptr`. Ownership can only be moved with `std::move(your_pointer)`.


<a href="#basics_move_semantics_">Click here to learn more about the Move Semantic.</a>

<br><br>

**std::shared_ptr**

Allows shared ownership of a resource.
The object is destroyed automatically when the last `shared_ptr` reference is gone.

```c++
#include <memory>
#include <iostream>

struct Entity {
	Entity() { std::cout << "Created\n"; }
	~Entity() { std::cout << "Destroyed\n"; }
};

int main() {
	auto e1 = std::make_shared<Entity>();
	{
		auto e2 = e1; // shared ownership
		std::cout << "Use count: " << e1.use_count() << '\n';
	} // e2 destroyed, count decreases

	std::cout << "Use count: " << e1.use_count() << '\n';
} // last shared_ptr destroyed -> object deleted
```

**std::weak_ptr**

A non-owning reference to a shared_ptr resource.<br>
Used to observe shared ownership without extending its lifetime.

```c++
#include <memory>
#include <iostream>

struct Entity {
	void speak() { std::cout << "Hello!\n"; }
};

int main() {
	auto shared = std::make_shared<Entity>();
	std::weak_ptr<Entity> weak = shared;

	if (auto locked = weak.lock()) { // try to get a shared_ptr
		locked->speak();
	}
} // shared destroyed -> weak becomes expired
```

<br><br>


Sometimes you also want to define your **own deleter** -> that is always needed when the compiler don't have the complete definition of the saved type, which is needed when deleting the object or you want that something happen when your pointer/object gets destroyed.

Here is the solution:
```cpp
auto sdl_controller_deleter = [](SDL_Gamepad* g) {
    if (g) SDL_CloseGamepad(g);
};

std::unique_ptr<SDL_Gamepad, decltype(sdl_controller_deleter)> controller(
    SDL_OpenGamepad(cid), sdl_controller_deleter
);

```
Or local:
```cpp
std::unique_ptr<SDL_Gamepad, decltype([](SDL_Gamepad* g){ if(g) SDL_CloseGamepad(g); })> controller(
                                                                                                SDL_OpenGamepad(cid),
                                                                                                [](SDL_Gamepad* g){ if(g) SDL_CloseGamepad(g); }
                                                                                            );
```

So you need a lambda function which takes an pointer from your type: 
`std::unique_ptr<YOUR_TYPE, decltype([](YOUR_TYPE* g){ if(g) SDL_CloseGamepad(g); })>`


<br><br>

<a name="basics_references_" href="#bascis_top_">^</a><br>
**References**<br>
References is a C++ feature which is not avaiable in C. References are variables which refer to another variable. The following example shows 2 variables which both have the same value and changes on both variables impact the value of the other variable. Notice that references are written with a & after the datatyp.
```c++
int i = 42;
int& r = i;
```
Helpful are references for example mutable functions, where the function changes its input/parameter values without returning something (a function with sideeffect). All parameter/input values are new values/variables in C++ -> even objects! This can be changed with references or pointer. (Notice that a pointer will also be created new but points to the same memory address and therefore works.<br>
Key difference to pointer: references can't have/refer to no value (easier handling) and need less ressources than pointer, because the reference is just another name for the same variable, and the pointer need a own memory address and the value is the memory address where it points to.<br>


<br><br>

<a name="basics_arrays_" href="#bascis_top_">^</a><br>
**Arrays**

> Please use modern dynamic arrays (std::vector from <vector>) which are described a bit further down. C-Style arrays should not be used anymore but can be interesting to know.

Arrays are a collection of n elements of the same datatype. An array can be thought as a primitive form of an list.<br>
Create and acces an array:
```c++
int arr_1[5] = {23, 4, -1, 34, 4};
int arr_2[5];
arr_2[0] = 12;

// heap allocated array
int* arr_3 = new int[5]{23, 4, -1, 34, 4};
```
Most important: arrays does not check for boundary and so can a wrong index cause memory corruption.<br>
An array is just a pointer to a memory address and is an old datatyp which should be replaced with newer versions of C++, but before we see these lets understand the access over the brackets.<br>
The number in the bracket by creating the array is from type size_t and defines how much memory/elements must be saved for the array. <br>
The number passed in the brackets during accessing an element just tells the compiler how much to count upwards to come to the element. So the arr variables points to one memory address and just adds a number to access another element, which is probably the reason, why an array can only keep values from the same datatyp.<br>
arr_1[0] == *(arr_1 + 0\*data_typ_size) -> arr_1 just returns the target memory address, though it is a pointer.

In modern C++ the old C-Style array is not the only option. The standard library also provides an array type and also vector and list types.
 - std::array -> constant array  (#include <array>)
 - std::vector -> dynamic array  (#include <vector>)
 - std::string -> dynamic char array  (#include <string>)

 std::array has a fixed size but provides some usefule methods:
 - size() -> Returns the number of elements (fixed at compile-time).
 - .at(index) -> Accesses an element with bounds checking. Throws exception if out of range.
 - .fill() -> Sets all elements to value.
 - .front() -> Returns the first element.
 - .back() -> Returns the last element.
 - .data() -> Returns a pointer to the first element (useful for C-style functions).
 ```c++
 #include <array>
 
 int main() {
 	std::array<int, 5> arr;
 	arr.fill(0);
 }
 ```

 <br><br>

 The dynamic array (std::vector) is the modern standard array, which should always be prefered over the C-Style array. The vector is a list, with no fixed size.
 ```c++
 #include <vector>
 
 int main(){
 	std::vector<int> vec = {1, 2};
 	vec.push_back(3);	// add an element
 }
 ```
Methods for Accesss:
 - .at(i) -> Access element (with bounds check)
 - .front() -> Returns the first element.
 - .back() -> Returns the last element.
 - .data() -> Returns a pointer to the first element (useful for C-style functions).

 Methods for modifying:
 - .push_back(x) -> Adds an value to the vector
 - .insert(pos, x) -> Adds an element on the given position
 - .pop_back() -> Remove last element
 - .erase(pos) -> Remove element at position
 - .clear() -> Remove all elements

 Methods for Size & Capacity
 - .size() -> Returns the number of elements
 - .capacity() -> Returns the allocated memory size
 - .resize(n) -> Resizes to n elements
 - .shrink_to_fit() -> Reduces capacity to match size
 - .reserve(n) -> Allocates memory for at least n elements (prevents reallocation overhead)

 Methods for Iterators:
 - .begin() -> Iterator to the first element
 - .end() -> Iterator to one past the last element
 - .rbegin() -> Reverse iterator (last element)
 - .rend() -> Reverse iterator (before first)

 Methods for Utility:
 - .empty() -> Returns true if vector is empty
 - .swap(otherVec) -> Swaps contents with another vector
 - .assign(n, x) -> Assigns n copies of x

 ```c++
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Basic Access
    std::cout << vec[2] << std::endl;  // Direct access (no bounds check)
    std::cout << vec.at(2) << std::endl; // Safe access (with bounds check)

    // Adding Elements
    vec.push_back(6);   // Adds 6 at the end
    vec.insert(vec.begin() + 2, 99); // Inserts 99 at index 2

    // Removing Elements
    vec.pop_back();    // Removes last element
    vec.erase(vec.begin() + 1); // Removes element at index 1

    // Size and Capacity
    std::cout << "Size: " << vec.size() << std::endl; // Number of elements
    std::cout << "Capacity: " << vec.capacity() << std::endl; // Memory allocated

    // Iterating Over Elements
    for (int num : vec) {
        std::cout << num << " ";  // Prints all elements
    }

    return 0;
}
 ```

 Lastly lets see methods of the string datatype.

 Methods for Accesss:
 - .at(i) -> Access element (with bounds check)
 - .front() -> Returns the first element.
 - .back() -> Returns the last element.
 - .data() -> Returns a pointer to the first element (useful for C-style functions).

 Methods for modifying:
 - .append(x) -> Adds an value to the string
 - .insert(pos, x) -> Adds an element on the given position
 - .erase(pos) -> Remove element at position
 - .replace(pos, len, x) -> Replace len chars from pos with x
 - .clear() -> Remove all elements

 Methods for searching and finding:
 - .find(x) -> Finds x (returns index or std::string::npos if not found)
 - .rfind(x) -> Finds last occurrence of x
 - .find_first_of(x) -> Finds first occurrence of any char in x
 - .find_last_of(x) -> Finds last occurrence of any char in x
 - .find_first_not_of(x) -> Finds first character not in x
 - .find_last_not_of(x) -> Finds last character not in x

 Methods for Extracting & Manipulating Substrings:
 - .substr(pos, len) -> Extract substring
 - .compare(x) -> Compare with another string (==, >, <)
 - .c_str() -> Convert to C-style string (const char*)

 Methods for Size & Capacity:
 - .length() -> Returns the number of characters
 - .size() -> Same as .length()
 - .capacity() -> Returns allocated memory size
 - .shrink_to_fit() -> Reduces capacity to fit size
 - .reserve(n) -> Allocates memory for n characters (prevents reallocations)

 Methods for Checking & Comparing:
 - .empty() -> Returns true if string is empty
 - str == x -> Checks equality
 - str != x -> Checks inequality

 Functions of String Module:
 - std::to_string(num) -> Converts number to string
 - std::stoi(str) -> Converts string to int
 - std::stof(str) -> Converts string to float
 - std::stod(str) -> Converts string to double


 ```c++
 #include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";

    // Accessing Characters
    std::cout << str[0] << std::endl;   // H (no bounds check)
    std::cout << str.at(1) << std::endl; // e (with bounds check)

    // Modifying String
    str.append("!!!");   // Adds "!!!" at the end
    str.insert(5, " C++"); // Inserts " C++" at index 5
    str.erase(5, 4);      // Removes 4 characters starting from index 5

    // Searching
    size_t pos = str.find("World"); // Finds "World" (returns index)
    size_t notFound = str.find("XYZ"); // Returns std::string::npos

    // Extracting Substring
    std::string sub = str.substr(7, 5); // "World"

    // Conversion
    std::string numStr = std::to_string(123); // Converts 123 -> "123"

    // Checking Length
    std::cout << "Length: " << str.length() << std::endl;

    return 0;
}
 ```


<br><br>

<a name="basics_collections_" href="#bascis_top_">^</a><br>
**Collections**<br>
We previously saw some important collections like the **Vector**. Here are some more with my most favourite, the unordered_map (Hash-Map or in Python would be a dictionary).

Notice: `emplace`/`emplace_back` constructs an element directly inside the container. You can also use `push_back` most of the time.<br>
Example:
```cpp
my_list.push_back(MyType(a, b));   // create object, then copy/move it
my_list.emplace_back(a, b);        // construct object directly in the list
```
Advantages of `emplace`:
- More efficient (no temporary object)
- Constructs elements in-place
- Works especially well for complex objects

| Container                                | Method                          |
| ---------------------------------------- | ------------------------------- |
| `std::list`, `std::vector`, `std::deque` | `emplace_back`, `emplace_front` |
| `std::map`, `std::unordered_map`         | `emplace`, `try_emplace`        |
| `std::set`                               | `emplace`                       |
| `std::queue`, `std::stack`               | `emplace`                       |


<br><br>

A **linked list** is a collection of pointers. So every element can be in another place in the memory.

```c++
#include <list>

std::list<int> my_list;

my_list.push_back(4);
my_list.push_back(6);
my_list.push_back(8);
my_list.push_front(2);

my_list.emplace_back(10);   // constructs directly
my_list.emplace_front(0);

my_list.front();     // first element
my_list.back();      // last element
my_list.pop_front();
my_list.pop_back();
my_list.size();
my_list.empty();
my_list.clear();
```

<br><br>

Another collection is the **Queue** which works with the FIFO (first in, first out). It is like a queue on a icecream shop.

```c++
#include <queue>

std::queue<int> my_q;

my_q.push(10);
my_q.push(20);
my_q.emplace(30);

my_q.front();   // access first element
my_q.back();    // access last element
my_q.pop();     // removes first element
```

<br><br>

The opposite is the **Stack**. It works with the LIFO priciple (last in, first out). The last element which got added will be the first which get out from the stack. Like a stack of papers on a table of a busy worker in the 80s.

```c++
#include <stack>

std::stack<int> my_stack;

my_stack.push(10);
my_stack.push(20);
my_stack.emplace(30);

my_stack.top();   // access top element
my_stack.pop();   // removes top element
```

<br><br>

Most performant data structures are the maps and hash maps. The difference is that maps are ordered and hash maps using hashing to allow unordered lists. They work with a key which lead to a value...like a dictionary.

```c++
#include <map>
#include <string>

std::map<int, std::string> months;

months.emplace(1, "January");
months.emplace(2, "February");

std::cout << months[2] << std::endl;

months.find(2);          // returns iterator
months.contains(2);     // C++20
months.erase(2);
months.size();
months.empty();
months.clear();
```

<br><br>

Hash-maps:
```c++
#include <unordered_map>
#include <string>

std::unordered_map<int, std::string> months;

months.emplace(1, "January");
months.emplace(2, "February");

std::cout << months[2] << std::endl;

// safer lookup
auto it = months.find(2);
if (it != months.end()) {
    std::cout << it->second << std::endl;
}

months.try_emplace(2, "NewValue"); // does NOT overwrite if key exists
months.at(2)
months[2]
// and functions most like std::map
```

> Using brackets for accessing values (`months[2]`) is most likely not recommended because with the sideffect that it will create an entry if no key is found and therefore the used key need to have an default-constructor (without any parameter) which is sometimes not given (for example if using a class as key which must get an parameter for construction, for example an ID).<br>In such cases it is better to use `months.at(2)` or `months.find(2)->second`.

When setting a value you should use `emplace` or `try_emplace` and do not use the brackets.

Benefits of using `try_emplace`:
- Constructs key-object in-place
- Only inserts if key doesn't exist
- No default constructor needed
- No temporary objects
- One lookup

`emplace`:
- No default constructor called
- May still create a temporary
- Does nothing if key exists (silently)

> only use brackets if handling primitve datatypes, like: `std::unordered_map<int, int>`


<br><br>

Important for collections is to itterate over them and this is sometimes not easy possible. For that we can use **Iterator** which are objects which help to traverse the object.

```c++
std::list<int> numbers;

numbers.emplace_back(2);
numbers.emplace_back(4);
numbers.emplace_back(6);

for (auto iter = numbers.begin(); iter != numbers.end(); ++iter) {
    std::cout << *iter << std::endl;
}

// or modern

for (int n : numbers) {
    std::cout << n << std::endl;
}

for (const int& n : numbers) {
    std::cout << n << std::endl;
}
```

For maps:
```c++
// Get an iterator to the element with the key 2 
std::map<int, std::string> iter = months.find(2); 

if (iter != months.end()) // This is only true if contains
    std::cout << iter->first << std::endl; // Outputs 2
    std::cout << iter->second << std::endl; // Outputs February
}

// for > C++20
if (months.contains(2)) 
    std::cout << month[2] << std::endl;  
}
```

 


<br><br>

<a name="basics_templates_" href="#bascis_top_">^</a><br>
**Templates**<br>
Templates are function defintions which use generic/at pre-compile time not defined datatypes.
Templates itself are no function and will first be added to your execution code, when a specific use of the function is there. If you call the template with for example int and string, 2 functions will be added at compile time.

It follows a perfect example with multiple use of templates. This can be defined only in a .h/.hpp file:

```cpp
#include <string>
#include <stdexcept>
#include <type_traits>  // std::is_arithmetic_v, std::is_same_v

template <typename T>
T getDefaultValue() {
    T default_value;
    if constexpr (std::is_arithmetic_v<T>) {
        default_value = 0;
    } else if constexpr (std::is_same_v<T, std::string>) {
        default_value = "";
    } else {
        throw std::logic_error("Type must be arithmetic or string!");
    }

    return default_value;
}

template <typename T>
T multiplyElement(const T& element, const int& multiplicator) {
    T multiplicationResult = getDefaultValue<T>();

    for (int i=0; i < multiplicator; ++i) {
        multiplicationResult += element;
    }

    return multiplicationResult;
};

template <typename T, typename U>
requires std::is_arithmetic_v<U>
T scaledSum(const T& x, const U& n) {
    T summation = multiplyElement(x, 0);
    for (int i=0; i <= n; ++i) {
        summation += multiplyElement(x, i);
    }

    return summation;
};
```


<br><br>

<a name="basics_namespaces_" href="#bascis_top_">^</a><br>
**Namespaces and Header Files**<br>
Namespaces are scopes in which are given variable names and function names set/available. <br>
You can also defining your own namespaces:
```c++
namespace my_namespace{
	// define here classes, functions, variables and more ...
}
```
Then the structures and variables are usable under the namespace name -> my_namespace::my_func();

If you want to use a another namespace / another library, you can import namespaces from the standard library (std) or from your own namespaces or external libraries.<br>
using the std namespace is direct available by:
```c++
#inculde <iostream>
// there are more namespaces in std!
...
```
External libraries or own code import need a header file (.h or .hpp).
These files define what the namespace contains. Notice that both the usage file and the defining file have to import the header file.
See this example:
compute.cpp:
```c++
#include "compute.h"

namespace math_utils {
    double computeArea(double radius) {
        return PI * radius * radius;  // Use the constant
    }
}
```

compute.h:
```c++
#pragma once    // stopps double imports

namespace math_utils {
    constexpr double PI = 3.14159265358979;  // Constant definition
    double computeArea(double radius);      // Function declaration
}
```

main.cpp:
```c++
#include <iostream>
#include "compute.h"

int main() {
    double radius = 5.0;
    double area = math_utils::computeArea(radius);  // Call function

    std::cout << "Circle with radius " << radius << " has area: " << area << std::endl;
    std::cout << "Using constant PI: " << math_utils::PI << std::endl;
    
    return 0;
}
```

Definitions inside the header file can be used also in the file which is linked to it! Example Game.h:
```c++
#pragma once

#include <cstdint>

// some definitions which can be directly used from linked file!
struct Coordinate {
   std::uint32_t x;
   std::uint32_t y;
};

enum class ConsoleInput {
   INVALID,
   LEFT,
   RIGHT,
   UP,
   DOWN
};


// functions defined by the linked Game.cpp file

void print_field(const Coordinate& player_position);
bool is_finish(const Coordinate& player_position);
void execute_move(Coordinate& player_position, const char move);
void play_game();
```

You can also import all names from a namespace with:
```c++
using namespace std;
```

But this is not recommended!

Also a unnamed namespace is only available for the current file -> so like a private variables, functions, ...
```c++
namespace{
auto my_private_int = 45;
//...
}

std::cout << my_private_int;
```

Overall namespaces give you easy control to what to export and what not and can be used differently and flexible.

Last notice: If you want to have one namespace with multiple libraries, like the std, then you can simply write a .cpp and a .h file for every lib and in the .h file you write the variables and functions to import inside a namespace and name this namespace like you want to name your lib.<br>
The opposite approach is also possible, that in the header file is no namespace but in the .cpp file you wrap everything inside your lib name namespace.<br>
It is also possible to have multiple header files from one file, so you could also create multiple namespaces from one file.<br>
As you might see, there are many possible ways how to implement your code. Namespaces are just a logic which can be used very flexible.

<br><br>

<a name="basics_std_" href="#bascis_top_">^</a><br>
**Standard Library (STD):**
It follows a overview about most namespaces of std, you can search online if you are interesting in one of them.<br>
Notice that all of these libraries are in the std namespace but get first loaded/imported if the specific lib is imported. This is practically done by defining different header files (for every lib one header file). 

Input/Output & Streams
- \<iostream\> – Standard I/O (cin, cout, cerr)
- \<fstream\> – File input/output streams
- \<sstream\> – String stream manipulation

Containers & Data Structures
- \<vector\> – Dynamic array (fast random access)
- \<array\> – Fixed-size array wrapper
- \<deque\> – Double-ended queue
- \<list\> – Doubly linked list
- \<forward_list\> – Singly linked list
- \<map\> – Sorted associative key-value container (RB-tree)
- \<unordered_map\> – Unordered key-value container (hash table)
- \<set\> – Sorted unique collection (RB-tree)
- \<unordered_set\> – Unordered unique collection (hash table)
- \<stack\> – LIFO stack
- \<queue\> – FIFO queue
- \<priority_queue\> – Heap-based priority queue
- \<tuple\> – Fixed-size heterogeneous collection

Algorithms & Utility Functions
- \<algorithm\> – Sorting, searching, min/max, transformations
- \<numeric\> – Numeric operations (accumulate, inner_product)
- \<functional\> – Function objects, lambda utilities
- \<utility\> – std::pair, std::move, std::forward, etc.
- \<ranges\> (C++20) – Range-based algorithms

Strings & Localization
- \<string\> – std::string, std::wstring
- \<string_view\> (C++17) – Non-owning string reference
- \<charconv\> (C++17) – Fast number-to-string conversion
- \<locale\> – Localization utilities
- \<codecvt\> (Deprecated in C++17) – Unicode conversions

Memory Management
- \<memory\> – Smart pointers (std::unique_ptr, std::shared_ptr)
- \<scoped_allocator\> – Memory allocation policies
- \<new\> – Low-level memory allocation (operator new)

Concurrency & Parallelism
- \<thread\> – Thread management
- \<mutex\> – Mutual exclusion locks
- \<shared_mutex\> (C++17) – Shared/read-write mutex
- \<atomic\> – Atomic operations (lock-free programming)
- \<condition_variable\> – Thread synchronization
- \<future\> – Asynchronous execution (std::async, std::promise)
- \<stop_token\> (C++20) – Stopping threads gracefully

Time & Date
- \<chrono\> – Time utilities (C++11)
- \<ctime\> – C-style time functions

Type information & Reflection
- \<type_traits\> – Type checking and manipulation (std::is_same, std::enable_if)
- \<typeinfo\> – Runtime type information (RTTI, typeid)
- \<concepts\> (C++20) – Constraints for templates

Math & Randomization
- \<cmath\> – Standard math functions (sin, cos, sqrt)
- \<random\> – Pseudo-random number generation
- \<numbers\> (C++20) – Mathematical constants like π and e

Filesystem & OS Interaction
- \<filesystem\> (C++17) – File and directory operations
- \<system_error\> – Error codes and exceptions
- \<cstdlib\> – C-style utilities (malloc, rand, exit)

Error Handling
- \<exception\> – Base exception classes
- \<stdexcept\> – Common exceptions (std::runtime_error, std::out_of_range)
- \<cassert\> – Debugging assertions
- \<cerrno\> – C-style error handling (errno)

Regular Expressions
- \<regex\> – Regular expressions

Networking
- \<net\> – Networking library

Coroutines
- \<coroutine\> – Coroutine support

<br><br>

<a name="basics_classes_" href="#bascis_top_">^</a><br>
**Classes**<br>
In object oritented programming, classes describe a class of which objects can be created. They get created in the heap with the new keyword, which calls the constructor method of the class. The destructor method will be called when the object is delected.<br>
Classes/Objects have the advantage of creating own data structures with well isolated methods.<br>
Passing an object to a function can be very ressource harming, due to the fact that functions always create a copy of the parameter. An common used practise is to pass an object with as **const reference** (const ClassName& var_name), this makes sure that the object can't get changed and it is the real object (not an copy).<br>
The access to attributes and functions is normally an '.' but if your object is an pointer than you need an '->' for accessing the variables and functions of your object. For example there is also an *this* which is a pointer to the current class object, if you want to make sure that an attribute or method is called from your object than use this->my_int. The '->' must be used because it is a pointer.

> Declare all available functions, classes, variables and methods in a .h/.hpp. Declase/implement all of these concept in a .cpp file with the same name. Sometimes you might want to declare and define everything in the .h/.hpp. 

Example class:<br>
complex.h
```cpp
#ifndef COMPLEX_H
#define COMPLEX_H

class Complex{
public:
	// Constructor
	Complex(float real, float imaginary);
    ~Complex() = default;
	
	void Negate();
	
private:
	float real;
	float imaginary;
};

#endif
```

complex.cpp
```cpp
#include <memory>

// Constructor
Complex::Complex(float real, float imaginary)
: real(real), imaginary(imaginary) {    // efficient init listing
// ...
}

void Complex::Negate() {
    // ...
}
	

// Run the code, maybe in a main.cpp

std::unique_ptr<Complex> c = std::make_unique<Complex>(1.0f, 2.0f);

c->Negate();
```

With this-> you can access an objects attributes and functions. If not setted the compiler will take a local attribute with this name and if there is no then taking the attribute from the class.

IMPORTANT Rule: If a member has no default constructor, it MUST be initialized in the initializer list because the compiler will first init all members and then run the code in the constructor. If given via init list, it will be executed during the construction. The `Complex(float real, float imaginary)` is an example for exactly this. If you try to make the same the standard way and assign the variables in the constructor, then the compiler will first try to compile all member variables with a standard constructor if there is no standard constructor it will throw an error.

There are also copy constructors which takes one object from the same class and gives a new object with the same values. C++ creates a copy method automatically but in case you use pointer you should write it by yourself, because the pointers will still reference to the same object -> calles shallow copy.<br>
Self declared deep copy constructor:

```c++
class Complex{
public:
	//...
	
	Complex(const Complex& other_obj) {
		this->real = other_obj.real;
	    this->imaginary = other_obj.imaginary;
	}

    // ...
};
```

Classes which handle dynamic allocated data (pointer, arrays, ...) should always define a destructor, copy constructor and  assignment operator. -> **rule of three**

Assignment operator are methods which define the behaviour if common signes like the + are used with the object. Here an example with the + sign. Notice that it have an + after the method name (our target sign) and it has the keyword 'friend' which defines that it can be used without an object (standalone).

```c++
friend Complex operator+(const Compley& a, Complex& b){
	return Complex(a.mReal + b.mReal, a.mImaginary+b.Imaginary);
}

Compley result = c1+c2;
```

There is also operator== for example. You can overload / define a behaviour for most likely any sign using the operator method. For example the stream lib from std does this with the \>\> signs to connect outputs.

Another important concept is the inheritance and abstract methods. Classes can have subclasses and to make sure that the subclass implement a method you can use `= 0` after the method head (see the example). The `virtual` keyword defines that the method can be inherited and therefore it makes clear which method to call if you have a object from subclass type but your variable is from the topclass (see example). The constructor can't be virtual because it can't be inherited and there is also no case where this could lead to confusion.<br>
The `:` after the classname head defines the class rom which to inherit.


```c++
#pragma once

#include <SDL3/SDL.h>

class Entity{
public:
	// virtual Entity; -> not possible
	virtual ~Entity;

	virtual void update() = 0;
	virtual void draw(SDL_Renderer* renderer) = 0;
};

class Player : public Entity{
	// ...
};

// ... in cpp file:
Entity* entity = new Player();
delete entity;  // What happens here?
```

<br><br>

In C++ automatic convertions are allowed. For example you have a constructor with one int parameter, than you can pass a int into a function which expects an object from this class and the int will be automatically converted into the object which is in most cases not good. The so called implicit version is not readable, confusing and can lead to missunderstanding when the class does not really represents the passed value.

Example:
```cpp
class Vec2 {
public:
    int x, y;

    // Normal constructor
    Vec2(int x, int y) : x(x), y(y) {}

    // Single-argument constructor (implicit)
    Vec2(int value) : x(value), y(value) {}
};
```

Now you can call:
```cpp
// some function
void printVec(Vec2 v) {
    std::cout << v.x << "," << v.y << std::endl;
}

printVec(5);  // <-- Works! Implicitly converts int → Vec2(5)
```

You can block such automatic conversions by using the `explicit` keyword before the constructor:

```cpp
class Vec2 {
public:
    int x, y;
    explicit Vec2(int value) : x(value), y(value) {}
};
```

Now this result in:
```cpp
printVec(5);  // Error :(
printVec(Vec2(5));  // Works :)
```


<br><br>

You can also call the constructor of the super class by using the initalizationlist:
```cpp
#ifndef ITEM_H 
#define ITEM_H 
#include <string> 

struct Item { 
    std::string name; 
    int sellIn; 
    int quality; 
}; 

class ItemUpdater { 
public: 
    ItemUpdater(Item item): item_(item) {}; 
    ItemUpdater(std::string name, int sellIn, int quality): item_(Item(name, sellIn, quality)) {}; 
    virtual ~ItemUpdater() = default; 
    
    virtual void updateQuality() = 0; 
    
protected: 
    Item item_; 
}; 

class StandardItemUpdater : public ItemUpdater { 
public: 
    StandardItemUpdater(Item item): {ItemUpdater(item)}; 
    StandardItemUpdater(std::string name, int sellIn, int quality): {ItemUpdater(name, sellIn, quality)}; 
    virtual ~StandardItemUpdater() = default; 
    
    virtual void updateQuality() override;     
}; 
    

#endif
```


<br><br>

You can also check if a class/struct is a given type via `typeid`:
```cpp
#include <typeinfo>
#include <iostream>

struct A {};
struct B {};

A a;
B b;

std::cout << (typeid(a) == typeid(A)) << std::endl; // true
std::cout << (typeid(a) == typeid(B)) << std::endl; // false
```

`typeid` returns a  `const std::type_info&`.

In some cases this can be wrong when using with inheritance and missing virtuals. <br>
Such a case is this:
```cpp
struct Base {};
struct Derived : Base {};

Base b = Derived{};
typeid(b) == typeid(Derived); // false
```

Another way is to use dynamic cast:

```cpp
#include <iostream>
#include <vector>
#include <memory>

struct Component {
    virtual ~Component() = default; // REQUIRED for dynamic_cast
};

struct RenderComponent : Component {
    void render() const {
        std::cout << "Rendering\n";
    }
};

struct PhysicsComponent : Component {
    void simulate() const {
        std::cout << "Simulating physics\n";
    }
};

// here we use dynamic cast
void process(Component* component) {
    if (auto* render = dynamic_cast<RenderComponent*>(component)) {
        render->render();
    }
    else if (auto* physics = dynamic_cast<PhysicsComponent*>(component)) {
        physics->simulate();
    }
}

// running code
int main() {
    std::vector<std::unique_ptr<Component>> components;

    components.push_back(std::make_unique<RenderComponent>());
    components.push_back(std::make_unique<PhysicsComponent>());

    for (const auto& c : components) {
        process(c.get());
    }
}
```

Use `typeid` when:
- You want exact type comparison
- You don't care about base/derived relationships
- Performance matters

Use `dynamic_cast` when:
- You want to know if an object is-a type
- You're working with polymorphism
- You care about inheritance hierarchies


<br><br>

<a name="basics_structs_" href="#bascis_top_">^</a><br>
**Structs**

Structs are also just classes in C++ and can everything what classes can BUT they are typically only used as more complex datatypes without (or only very few) methods.<br>
While in languages like python you can mix datatypes easily (in C++ also possible but way harder), in C++ the most comfortable but still nice way is with structs.

Here is an practical example:
```cpp
struct Window {
    std::tuple<int, int> position{ 0, 0 };
    std::tuple<int, int> size{ 512, 512 };
    bool is_accessed{ true };
    bool is_activated{ true };
};

struct ActiveState {
    std::vector<Key> keys;
    std::vector<MouseButton> mouse_buttons;
    std::unordered_map<int, std::vector<ControllerButton>> controller_buttons;
    std::unordered_map<int, std::vector<ControllerAxis>> controller_axis;
};
```

They use the `struct` keyword, are very straight forward. Every member/attribute is `public` by default (while in classes the default is `private`).

Typical characteristics:
- Public data members
- Lightweight
- No strong invariants
- Often POD / aggregate-like
- Used for data transfer, math types, configs

It is also often use with aggregate initialization:
```cpp
struct Color {
    int r, g, b;
};

Color c{255, 128, 0};
```

> A struct is a class that doesn't hide its data by default. -> C++ has only "classes", struct just flips the defaults.


<br><br>

<a name="basics_class_methods" href="#bascis_top_">^</a><br>
**Class Methods**

You can define many special methods for your classes to define behaviour for example when using brackets on your class `my_obj[0]`. Here is an overview of the most common methods in C++ for your classes.

Object Lifetime (standard 5/6 methods)

| Purpose                            | Method Signature                         | Notes                                     |
| ---------------------------------- | ---------------------------------------- | ----------------------------------------- |
| Default constructor                | `ClassName()`                            | Can be implicitly deleted or generated    |
| Destructor                         | `~ClassName()`                           | Should be virtual if class is polymorphic |
| Copy constructor                   | `ClassName(const ClassName&)`            | Deep copy logic                           |
| Copy assignment                    | `ClassName& operator=(const ClassName&)` | Handle self-assignment                    |
| Move constructor                   | `ClassName(ClassName&&)`                 | Transfers ownership                       |
| Move assignment                    | `ClassName& operator=(ClassName&&)`      | Usually `noexcept`                        |
| Defaulted destructor (Rule of 0/6) | `= default`                              | When RAII members handle everything       |


> Rule of 5: if you define one, you should define all of them -> destructor + copy/move constructor + copy/move assignment
> Rule of 0: just let every of the 5 default

<br><br>

Comparison Operators

| Operator      | Signature                                 |
| ------------- | ----------------------------------------- |
| Equality      | `bool operator==(const ClassName&) const` |
| Inequality    | `bool operator!=(const ClassName&) const` |
| Less-than     | `bool operator<(const ClassName&) const`  |
| Less-equal    | `bool operator<=(const ClassName&) const` |
| Greater-than  | `bool operator>(const ClassName&) const`  |
| Greater-equal | `bool operator>=(const ClassName&) const` |

Three-way Comparison (C++20)

| Operator                | Signature                                  | Notes                     |
| ----------------------- | ------------------------------------------ | ------------------------- |
| Spaceship               | `auto operator<=>(const ClassName&) const` | Generates all comparisons |
| Equality (still needed) | `bool operator==(const ClassName&) const`  | Required for `<=>`        |


<br><br>


Stream Operators (I/O)

| Operator | Signature                                                          | Notes    |
| -------- | ------------------------------------------------------------------ | -------- |
| Output   | `friend std::ostream& operator<<(std::ostream&, const ClassName&)` | Printing |
| Input    | `friend std::istream& operator>>(std::istream&, ClassName&)`       | Parsing  |

<br><br>

Arithmetic Operators

| Operator       | Signature                                     |
| -------------- | --------------------------------------------- |
| Addition       | `ClassName operator+(const ClassName&) const` |
| Subtraction    | `ClassName operator-(const ClassName&) const` |
| Multiplication | `ClassName operator*(const ClassName&) const` |
| Division       | `ClassName operator/(const ClassName&) const` |
| Modulo         | `ClassName operator%(const ClassName&) const` |


<br><br>

| Operator   | Signature                                 |
| ---------- | ----------------------------------------- |
| Add-assign | `ClassName& operator+=(const ClassName&)` |
| Sub-assign | `ClassName& operator-=(const ClassName&)` |
| Mul-assign | `ClassName& operator*=(const ClassName&)` |
| Div-assign | `ClassName& operator/=(const ClassName&)` |


<br><br>

Unary Operators

| Operator          | Signature                     | Meaning           |
| ----------------- | ----------------------------- | ----------------- |
| Unary plus        | `ClassName operator+() const` | Identity          |
| Unary minus       | `ClassName operator-() const` | Negation          |
| Logical NOT       | `bool operator!() const`      | Custom truthiness |
| Bitwise NOT       | `ClassName operator~() const` | Inversion         |
| Prefix increment  | `ClassName& operator++()`     | `++x`             |
| Postfix increment | `ClassName operator++(int)`   | `x++`             |
| Prefix decrement  | `ClassName& operator--()`     | `--x`             |
| Postfix decrement | `ClassName operator--(int)`   | `x--`             |

<br><br>

Assignment & Access

| Operator        | Signature                           | Purpose           |
| --------------- | ----------------------------------- | ----------------- |
| Subscript       | `T& operator[](size_t)`             | Array-like access |
| Const subscript | `const T& operator[](size_t) const` | Read-only         |
| Function call   | `Return operator()(Args...)`        | Functor           |
| Dereference     | `T& operator*()`                    | Pointer-like      |
| Arrow           | `T* operator->()`                   | Smart pointers    |

<br><br>

Conversion Operators

| Conversion          | Signature                        | Notes                 |
| ------------------- | -------------------------------- | --------------------- |
| Implicit conversion | `operator TargetType() const`    | Dangerous if implicit |
| Explicit conversion | `explicit operator bool() const` | Common & safe         |

<br><br>

Memory Management (Rare but Important)

| Operator     | Signature                       |
| ------------ | ------------------------------- |
| Allocation   | `void* operator new(size_t)`    |
| Deallocation | `void operator delete(void*)`   |
| Array new    | `void* operator new[](size_t)`  |
| Array delete | `void operator delete[](void*)` |

<br><br>

Bitwise Operators

| Operator    | Signature                                     |                           |
| ----------- | --------------------------------------------- | ------------------------- |
| AND         | `ClassName operator&(const ClassName&) const` |                           |
| OR          | `ClassName operator                           | (const ClassName&) const` |
| XOR         | `ClassName operator^(const ClassName&) const` |                           |
| Left shift  | `ClassName operator<<(int) const`             |                           |
| Right shift | `ClassName operator>>(int) const`             |                           |
| AND-assign  | `ClassName& operator&=(const ClassName&)`     |                           |
| OR-assign   | `ClassName& operator                          | =(const ClassName&)`      |

<br><br>

Miscellaneous / Less Common

| Operator          | Signature                               |
| ----------------- | --------------------------------------- |
| Comma             | `ClassName operator,(const ClassName&)` |
| Pointer-to-member | `operator->*`                           |
| Placement new     | `void* operator new(size_t, void*)`     |



<br><br>

<a name="basics_brace_init_" href="#bascis_top_">^</a><br>
**Brace Initialization**

In modern C++ you can not only use the standard equal sign initialization but also a brace initialization.

Let's start with showing this in practise:

```cpp
struct Window {
    int width{512};        // brace initialization
    int height = 512;      // equals sign initialization
    bool active{true};
};
```

> Notice that you propably already saw this brace init. Even on this quick guide we often used that init method.

In many cases there is no difference visible but let me list some differences:<br>
- brace init does not perform silent type conversions:
    ```cpp
    int x{3.5}; // ERROR: narrowing conversion from double to int
    int y = 3.5; // Allowed, silently truncates to 3
    ```
- brace init can be used to init with default values:
    ```cpp
    int x{};
    int y = // Equal Init has nothing like that!
    ```
- uniform init of many different types:
    - Built-in types: `int x{5};`
    - Objects: `std::tuple<int,int> t{0,0};`
    - Arrays: `int arr[3]{1,2,3};`
    - Containers: `std::vector<int> v{1,2,3};`

The difference behind the scenes is that the equal init will call the `copy-initialization` and the brace init will call the `direct-list-initialization`.

```cpp
class MyBool {
public:
    bool value;
    MyBool(bool v) : value(v) {}             // constructor
    MyBool(const MyBool& other) { value = other.value; } // copy constructor
};

MyBool b{true};   // direct-list-initialization: calls only constructor MyBool(bool)
MyBool c = b;     // copy-initialization: calls copy constructor (just as reference here)
MyBool b = MyBool(true);  // copy-initialization: temporary object + copy constructor
```

I think the code above explains everything clearly. The equal initialization always comes with the call of the copy constructor (and sometimes a temproray object). While the brace initialization does only call the constructor which is more efficient.


> Notice that modern C++ compilers might use the **Mandatory Copy Elision** to compile equal-initialization statements the same as they would with brace-initialization. So it depends on the used compiler how the statements/expressions are actually compiled (makes sense I guess).

Small general clearification:
- Expression: Something which evaluates to a value. Example: `1+2/x`, `func()`, `"Hello" + " World"`
- Statement: A line of code which does something. Example: `return;`, `x = func()`, `while (x < 5) { ... }`


<a name="basics_move_semantics_" href="#bascis_top_">^</a><br>
**Move Semantics**

`std::move` is most likely used with `std::unique_ptr` (Unique Smartpointer) where only one variable hold the reference to the heap-memory (object). It comes from `#include <utility>` and what happens is pretty easy.<br>

// During  or which do nothing else than a cast from rvalue to lvalue.

Let's say we have 2 ways we want to xray inside of C++ compiler:
1. ```cpp
    ResourceHandle a;

    ResourceHandle b = createResourceHandle();

    ResourceHandle c = std::move(a);
    ```
2. ```cpp
    ResourceHandle a;
    ResourceHandle b;

    b = std::move(a);
    ```

There are two basic ways to assign a value in C++, and at first glance the difference may seem small, but the compiler handles them differently. When creating a new object, like ResourceHandle `c = std::move(a);` or `ClassName b = a;`, the move constructor (spoiler) or copy constructor is called, respectively. When assigning to an existing object, like `b = std::move(a);` or `b = a;`, the move assignment operator or copy assignment operator is called.

So I already spoilered you `std::move` does just call another method which you can define by yourself and in C++ there are 2 different types of assignments, so we can define 2 different move methods and if we change one we should change the other too.<br>
Here is the `solution` of our 2 examples.

1. ```cpp
    ResourceHandle a;

    // 1. Moving a temporary returned from a function
    ResourceHandle b = createResourceHandle(); // move constructor called

    // 2. Using std::move on an existing object to initialize a new one
    ResourceHandle c = std::move(a);           // move constructor called
    ```
2. ```cpp
    ResourceHandle a;
    ResourceHandle b;

    // Move assignment
    b = std::move(a);   // move assignment operator called
    ```

Basic Signature of the 2 move methods and for reference the 2 standard methods which are called if not using `std::move`:
| Operation                | Standard signature                                 | Usage |
| --- | --- | --- |
| Copy constructor         | `ClassName(const ClassName& other)`                | `ClassName b = a` and `ClassName b = ClassName()` |
| Copy assignment operator | `ClassName& operator=(const ClassName& other)`     | `ClassName b; b = a` |
| Move constructor         | `ClassName(ClassName&& other) noexcept`            | `ClassName b = std::move(a)` |
| Move assignment operator | `ClassName& operator=(ClassName&& other) noexcept` | `ClassName b; b = std::move(a)` |

<br><br>

> Notice that `ClassName b = ClassName()` is the same as `ClassName b = a`, because it creates a temporary object and then calls the copy constructor. For direct constructor without the temporary object and calling the copy-constructor: use brace-init `ClassName b{}`.


But what happens inside of this other assignment/constructor method?<br>
First let me show you the code:
```cpp
ResourceHandle::ResourceHandle(ResourceHandle&& other) noexcept {
    this->resource_ = other.resource_;
    other.resource_ = nullptr;
}



ResourceHandle& ResourceHandle::operator=(ResourceHandle&& other) noexcept {
    if (this != &other) {
        if (this->resource_ != nullptr) {
            releaseResource(this->resource_);
        }
        this->resource_ = other.resource_;
        other.resource_ = nullptr;
    } 
    return *this;
}
```

We just have to take the pointer to the heap-memory (a heap-address) and set the other object pointer to null. Ad here we can see the little difference from constructor and assignment method because in the assignment we have additionally have to check if the other object is not ourself and we also have to release/delete the current pointer/ressource the object have because when we call assignment operator then our object already exist and could already have another ressource. And when we call the constructor we also can't pass the same object because the object does not exist, we are about to create it the first time, which makes our live a little bit more relax.

Maybe you noticed that the biggest and most important difference is `ResourceHandle&&`...as you might know `ResourceHandle&` is a reference to the object and not a copy so it is the actual object, but what if there 2x&? It is still a reference but not from a normal object (also called `lvalue`) but it is a reference from an `rvalue`. So let's understand what a reference, a lvalue and a rvalue is and then we should have every part of the puzzle.<br>
The following code creates a lvalue reference. A reference just says "this new variable x is now an alias for variable y". So the compiler treat both variables as they would be the same.
```cpp
int x = 42;
int& ref = x; // ref is a reference to x

ref = 100;
std::cout << x; // prints 100
```
So far so easy. An `lvalue` is everything which have an **persistent memory address**. For example most named variables are saved persistent into the memory address (= lvalues). Here an practical example:
```cpp
int x = 10; // x is an lvalue
int* p = &x; // you can take its address
```
`rvalue`'s on the other side are values which are only **temporary** and you can often only read them but this is not a must.

With that following datatyp signatures are for `lvalues`/`rvalues` references:
| Reference type     | What it can bind to | Typical use                      |
| --- | --- | --- |
| `T&` (lvalue ref)  | lvalues only        | Modify existing object           |
| `const T&`         | lvalues and rvalues | Read-only access, avoids copying |
| `T&&` (rvalue ref) | rvalues only        | Move / steal resources           |

Lastly one hint towards the unique smartpointers, because they are often used in `std::move` but the unique pointer has a persistent memory address and therefore is an lvalue and exactly that is the point. The move operator casts the old unique pointer reference into an rvalue because it only accepts rvalue references and therefore the old pointer will be casted into an rvalue. This is important because the whole point of the unique smartpointer is that there is always only 1 variable holding the pointer.<br>
Let's see an example for this:
```cpp
std::unique_ptr<int> p1 = std::make_unique<int>(42);
std::unique_ptr<int> p2 = p1; // error: copy constructor deleted, a unique pointer is move-only!
```
Ok now let's see the way it works:
```cpp
std::unique_ptr<int> p1 = std::make_unique<int>(42);
std::unique_ptr<int> p2 = std::move(p1); // calls the move constructor + casts p1 to nullptr because it value gets rvalue
```
The tricky part is to understand that `T&&` gives the compiler the permission to steal ressources even id the actual expression is an lvalue. 

Let's go through it a last time, to put together all the puzzle pieces with our previous example:
```cpp
std::unique_ptr<int> p1 = std::make_unique<int>(42);
std::unique_ptr<int> p2 = std::move(p1);
```
In line 1 our first unique smartpointer gets created, by creating a temporary (rvalue) object and then automatically calling the move-constructor operator, because it is an rvalue. Notice that modern C++ compiler might use the Mandatory Copy Elision to compile such statements the same as it would with brace-initialization. <br>
In line 2 it get more interesting. Here we call `std::move` which lead to calling the move constructor not the copy constructor and this method takes the p1 value as rvalue reference while p1 stays an lvalue in reality but with that we have the permission to reference to the same pointer-value and then set p1 to nullptr. Then we are finish.

> This gets us to other breaking news: In modern C++ the compiler most likely uses the move-constructor in complex datatypes (hint: if not using the Mandatory Copy Elision...yes it get even more complicated). For example we have a class `T`, then this code: `T a = T();` will create an temporary object and therefore the compiler most likely prefares to use the move constructor in such cases but notice that he also can use the normal copy constructor because the signature have const `T& operator=(const T& t)` which is also ok for rvalues becuase it is read-only.<br>Primitive datatypes are not affected by this because they are not classes and can be only copied and not moved because of this (image the bits are literally copied).

I hope this little explanation was helpful, it is not a easy topic and you have to think about it before understanding it...in the end it is pretty easy.


<br><br>

<a name="basics_error_handling_" href="#bascis_top_">^</a><br>
**Error Handling**

Modern C++ encourages safe and expressive error handling that avoids undefined behavior and ensures resources are released automatically.

**Exceptions**

Exceptions are the standard mechanism to report and handle errors in modern C++.

```c++
#include <stdexcept>
#include <iostream>

int divide(int a, int b) {
	if (b == 0)
		throw std::invalid_argument("Division by zero");
	return a / b;
}

int main() {
	try {
		std::cout << divide(10, 0) << '\n';
	} 
	catch (const std::exception& e) {
		std::cerr << "Error: " << e.what() << '\n';
	}
}
```

Common exceptions (`<stdexcept>`):
- `std::invalid_argument`
- `std::out_of_range`
- `std::runtime_error`
- `std::logic_error`
- `std::overflow_error`

Throwing an exception is easy:
```c++
#include <stdexcept>

throw std::runtime_error("Cannot open file");
```

You can mark functions as noexcept when they are guaranteed not to throw.
```c++
void logMessage(const std::string& msg) noexcept {
	std::cout << msg << '\n';
}
```

Example for files after the *Resource Acquisition Is Initialization* (RAII):
```c++
#include <fstream>
#include <stdexcept>

void writeFile() {
	std::ofstream file("output.txt");
	if (!file)
		throw std::runtime_error("Cannot open file");
	file << "Hello Modern C++!\n";
} // file closed automatically here
```

> Always manage resources (files, memory, sockets, etc.) with RAII objects or smart pointers (`std::unique_ptr`, `std::shared_ptr`).


<a name="basics_cpp_paradigms_" href="#bascis_top_">^</a><br>
**Choosing the right Programming Paradigm in C++**<br>

C++ is a multi-paradigm language -> you can use procedural, object-oriented, generic, and functional styles in the same project.<br>
Choosing the right paradigm for each part of your system is key to writing clean, efficient, and maintainable code.

<br><br>

\>\>\> Procedural Programming (Imperative)

Procedural Programming is like a sub-category of imperative programming and uses function-calls (outside of a class) are primary logic. Imperative programming uses only statements for logic.

> When to use: small, self-contained logic or low-level operations.

- Use for simple algorithms, math routines, and performance-critical code.
- Keeps execution flow explicit and easy to debug.
- Ideal for utilities, data transformations, and embedded code.
- Avoid over-engineering - sometimes a clean loop is all you need.

Example:
```cpp
double computeAverage(const std::vector<double>& values) {
    double sum = 0.0;
    for (double v : values) sum += v;
    return sum / values.size();
}
```

<br><br>

\>\>\> Object-Oriented Programming (OOP)

OOP encapsulate data and logic into object-units defined by classes and methods. And these classes can also share and use code from top/base-classes, to reduce redundancy, which is primarly important for similiar code with interferences but with partwise variations (for example: every dog have 4 legs and share much data and logic and therefore much can be defined for all dogs and sub-classes define specific concepts).

> When to use: modeling entities that have state and behavior.

- Good for systems with clear data hierarchies or interacting entities (e.g., game objects, UI elements).
- Encapsulate data and logic within classes.
- Use inheritance only when the relationship is a true “is-a”.
- Prefer composition (“has-a”) over inheritance to increase flexibility.

Example:
```cpp
class Renderer {
public:
    void Render(const Mesh& mesh);
};

class SceneObject {
public:
    Renderer renderer;
    Mesh mesh;
    void Draw() { renderer.Render(mesh); }
};
```

<br><br>

\>\>\> Generic / Template Programming

> When to use: reusable logic that’s independent of data type.

- Great for containers, algorithms, and utilities.
- Enables compile-time polymorphism with zero runtime overhead.
- Combine with concepts (C++20+) for clearer constraints and errors.

Example:
```cpp
template<typename T>
concept Number = std::is_arithmetic_v<T>;

template<Number T>
T Add(T a, T b) { return a + b; }
```

<br><br>

\>\>\> **Functional Programming**

C++ is not a functional programming language but have concepts of functional programming. In functional programming functions are the key element but in a math way. So it should be independed to external states (`const` -> const-correctness) and also should not effect external states (no side-effects -> pure functions).

This also include:
- Recursion: A function calls itself.
- High Order Functions: functions as parameter. This is more complicated with C++.

> When to use: data processing, transformations, and concurrency.

- Avoids side effects -> easier testing and parallelization.
- Encourages use of lambdas, std::transform, std::accumulate, and std::ranges.
- Combine with immutability (const) for safe, predictable code.

Example:
```cpp
std::vector<int> squared;
std::ranges::transform(values, std::back_inserter(squared),
                       [](int v){ return v * v; });
```

<br><br>

\>\>\>



<br><br>

<a name="basics_best_practices_" href="#bascis_top_">^</a><br>
**Best Practices**

These guidelines help maintain code that is safe, maintainable, and efficient.<br>
Modern C++ offers many features that make manual memory management and unsafe patterns unnecessary.<br>
Be carefully with C++ legacy code! And be careful with AI-generated code, which is often not maintainable and only "functional".

**General Principles:**
- Always use modern C++ (C++17 or newer) - safer and more expressive
- Prefer clarity and correctness over cleverness
- Keep functions, classes, and modules small and focused

**Parameter Passing:**
- Pass non-trivial types as `const` & (read-only) or by reference/pointer if modification is needed
- Avoid passing by value unless the function truly needs a copy
- Mark parameters as `const` whenever the function should not modify them

**Modern Best Practices:**
- Prefer `std::unique_ptr` and `std::make_shared` over raw pointers
- Use RAII and smart containers instead of manual memory management
- Use `auto`, `constexpr`, and `enum class` for clarity and safety
- Prefer range-based loops and standard algorithms (`std::for_each`, `std::transform`)
- Use move semantics to avoid unnecessary copies
- Favor immutability (`const`) and references over raw pointers
- Use modules (C++20+) to reduce compile time and dependency complexity
- Avoid macros for logic - use `constexpr` or inline functions instead
- Avoid manual `new`, `delete`, and `malloc`

**Memory Safe:**
- Avoid side effects in functions; keep them pure when possible
- Always initialize variables before use
- Avoid undefined behavior and non-deterministic patterns

**Testing and Maintainability:**
- Follow a test-driven or at least test-supported approach
      -  Write unit tests before or after implementing functionality
- Clean and refactor after adding new code - technical debt accumulates fast
    - With every line of new code, you increase your technical debt. Or in other words: you make your code uglier with every new code
    - After new code/new features, it is important to take time to clean the new (and maybe the old code), and maybe refactor some parts. Making some parts more modular or using polymorphy and more smaller functions.
- Modularize and generalize where duplication occurs (DRY principle)

> Remember on your technical debts! It is often seen that code gets worse and worse over time which is completly normal and that is the reason why for example live-service games get more bugs after some years then at the beginning. So remeber to take some time for clean-up and refactoring!

**Function Design:**
- Each function should have only one responsibility
- Keep functions short (ideally <= 10 lines)
- Avoid more than 3 parameters if possible
- Minimize branching (few `if` / `switch` paths)
- Function names should be verbs (e.g., `loadFile()`, `computeAverage()`).

**Variables should:**
- Name variables as carefully as you would name your first-born
- Use expressive, meaningful names
- Be consistent: choose camelCase or snake_case, not both
- Avoid abbreviations unless widely recognized (idx, pos, ...)

**Class Design:**
- Class names should be nouns and singular
- Inheritance should only represent a clear “is-a” relationship
- Prefer composition and modularity over deep inheritance chains
- Modularity should be prevert over polymorphy

**Modularity and Code Reuse:**
- Prefer modular, reusable code through:
    - Functions
    - Templates / Generics
    - Polymorphism (only when needed)

> **Rule of thumb:** Modularity should be preferred over polymorphism -> choose the right paradigm for the task and combine them for maximum clarity and efficiency.

Also choose the right programmin paradigm for the right tasks. <a href="#basics_cpp_paradigms_">See this chapter</a>.

> These are only rules which should be targeted during developement. There are many edge cases where it is good to break some of these rules, but it is important that this happens conscious.



<a name="basics_modern_cpp_" href="#bascis_top_">^</a><br>
**Modern C++**<br>

Modern C++ refers to the evolution of the C++ language starting with C++11 and continuing through C++14, C++17, C++20, and C++23.
The goal of modern C++ is to write safer, cleaner, and more expressive code - without sacrificing performance.

Modern C++ encourages:
- **RAII (Resource Acquisition Is Initialization)** - automatic resource management
- **Value semantics** - prefer copying/moving over raw pointers
- **Type inference** - let the compiler deduce types
- **Zero-cost abstractions** - high-level code that compiles to optimal machine code
- **Safety through ownership and immutability** - avoid manual memory handling

**Key Features**
- **Type Inference**
    ```c++
    auto x = 42;           // deduced as int
    auto message = "Hi!";  // deduced as const char*
    ```
    Improves readability and reduces redundancy.<br>
    Use auto for clarity, not to hide meaning.
- **Range-based Loops**
    ```c++
    std::vector<int> nums{1, 2, 3, 4};
    for (int n : nums) {
        std::cout << n << ' ';
    }
    ```
- **Smart Pointers (RAII)**
    ```c++
    #include <memory>
    auto ptr = std::make_unique<int>(10);  // automatically deleted
    ```
- **Move Semantics**<br>Enables efficient transfer of ownership for large objects.
    ```c++
    std::vector<int> a{1, 2, 3};
    std::vector<int> b = std::move(a);  // move instead of copy
    ```
- **Lambdas**<br>Inline anonymous functions with captures.
    ```c++
    auto square = [](int x) { return x * x; };
    std::cout << square(5);
    ```
    Useful in algorithms and functional-style code.
- **(auto,) decltype, and constexpr**
    ```c++
    constexpr int add(int a, int b) { return a + b; }  // compile-time evaluation
    decltype(auto) getValue() { return 42; }          // deduce return type
    ```
    Allows compile-time computations and stronger type safety.
- **Structured Bindings (C++17)**
    ```c++
    std::pair<int, std::string> p{1, "A"};
    auto [id, name] = p;
    ```
    Makes tuple and pair unpacking clean and readable.
- **Ranges and Concepts (C++20)**
    ```c++
    #include <ranges>
    #include <vector>
    #include <iostream>

    std::vector<int> v{1, 2, 3, 4, 5};
    for (int n : v | std::views::filter([](int x){ return x % 2 == 0; })) {
        std::cout << n << ' ';
    }
    ```
    Concepts add compile-time constraints to templates:
    ```c++
    template <std::integral T>
    T add(T a, T b) { return a + b; }
    ```
- **Coroutines (C++20)**<br>Used for asynchronous programming and generators.
    ```c++
    #include <coroutine>
    #include <iostream>

    auto generator() -> std::generator<int> {
        for (int i = 0; i < 3; ++i)
            co_yield i;
    }
    ```
- **std::expected (C++23)**<br>A safer alternative to exceptions for predictable errors.
    ```c++
    #include <expected>
    #include <string>

    std::expected<int, std::string> divide(int a, int b) {
        if (b == 0) return std::unexpected("Division by zero");
        return a / b;
    }
    ```

> Also do not use C-Style arrays, instead use `std:.vectors`!

Modern C++ combines *high performance* with *high-level expressiveness*.
It encourages writing code that is:
- **Safe** (no memory leaks or dangling pointers)
- **Readable** (less boilerplate)
- **Efficient** (no runtime overhead)
- **Composable** (works well with templates, ranges, and RAII)


<br><br>

<a name="basics_examples_" href="#bascis_top_">^</a><br>
**Examples**<br>
It follows some example cpp files.

- [Hello World](./00_hello_world/main.cpp)
- Variables, Datatypes and Logic
  - [Variables](./src/basics/01_variables_datatypes_logic/variables.cpp)
  - [Data Types](./src/basics/01_variables_datatypes_logic/datatypes.cpp)
  - [User Input](./src/basics/01_variables_datatypes_logic/user_input.cpp)
  - [If Else](./src/basics/01_variables_datatypes_logic/if_else.cpp)
  - [Ternary](./src/basics/01_variables_datatypes_logic/ternary_operator.cpp)
  - [For Loops](./src/basics/01_variables_datatypes_logic/for_loop.cpp)
  - [While Loops](./src/basics/01_variables_datatypes_logic/while_loop.cpp)
  - [Functions](./src/basics/01_variables_datatypes_logic/functions.cpp)
  - [Recursion](./src/basics/01_variables_datatypes_logic/recursion.cpp)
  - [Overloaded Funtions](./src/basics/01_variables_datatypes_logic/function_overloading.cpp)
  - [Templates](./src/basics/01_variables_datatypes_logic/template.cpp)
  - [Pre and Post Increment](./src/basics/01_variables_datatypes_logic/post_and_pre_increment.cpp)
  - [Constant Variables](./src/basics/01_variables_datatypes_logic/const.cpp)
  - [Static Local Variables](./src/basics/01_variables_datatypes_logic/static_local_var.cpp)
  - [Casting](./src/basics/01_variables_datatypes_logic/casting.cpp)
  - [Auto Keyword](./src/basics/01_variables_datatypes_logic/auto_keyword.cpp)
- Arrays, Pointer and References
  - [Arrays](./src/basics/02_pointer_and_arrays/arrays.cpp)
  - [Strings](./src/basics/02_pointer_and_arrays/string.cpp)
  - [Multidimensionale Arrays](./src/basics/02_pointer_and_arrays/multidimensional_arrays.cpp)
  - [Arrays in C++ Style](./src/basics/02_pointer_and_arrays/arrays_cpp_style.cpp)
  - [Pointer](./src/basics/02_pointer_and_arrays/pointer.cpp)
  - [Heap in C Style](./src/basics/02_pointer_and_arrays/heap_c_style.cpp)
  - [Nullpointers](./src/basics/02_pointer_and_arrays/nullpointers.cpp)
  - [Pointer Arrays](./src/basics/02_pointer_and_arrays/pointer_arrays.cpp)
  - [References](./src/basics/02_pointer_and_arrays/references.cpp)
  - [Argc and Argv](./src/basics/02_pointer_and_arrays/argc_argv.cpp)
- Enums, Structs and Namespaces
    - [Enum and Switch (C-Style)](./src/basics/03_enum_structs_and_namespaces/Enum_and_Switch.cpp)
    - [Enum Class](./src/basics/03_enum_structs_and_namespaces/Enum_Class.cpp)
    - [Structures](./src/basics/03_enum_structs_and_namespaces/Struct.cpp)
    - [Namespaces](./src/basics/03_enum_structs_and_namespaces/Namespaces.cpp)
- ...



Games/Projects:
- [Guessing Game](./games/guessing_game/)
- [Game 1](./games/computer_game_1/)
- [Game 2](./games/computer_game_2/)
- ...



<br><br>

<a name="basics_common_errors_" href="#bascis_top_">^</a><br>
**Common Errors**

Compile-Time Errors (Syntax & Type Issues)

| Error                            | Cause                                  | How to Fix                     |
| -------------------------------- | -------------------------------------- | ------------------------------ |
| `expected ';'`                   | Missing semicolon                      | Add `;` at end of statement    |
| `undeclared identifier`          | Variable not declared or wrong scope   | Declare before use / fix scope |
| `cannot convert 'X' to 'Y'`      | Type mismatch                          | Use correct type or cast       |
| `no matching function for call`  | Wrong arguments                        | Match function signature       |
| `invalid use of incomplete type` | Forward declaration without definition | Include full header            |
| `expected ')' before '{'`        | Mismatched parentheses                 | Fix bracket pairing            |
| `redefinition of 'X'`            | Defined twice                          | Remove duplicate definition    |
| `Member not default-constructible` | Initialized in constructor body      | Use initializer list           |



<br><br>

Linker Errors

| Error                             | Cause                                     | How to Fix                                    |
| --------------------------------- | ----------------------------------------- | --------------------------------------------- |
| `undefined reference to function` | Function declared but not defined         | Implement function                            |
| `multiple definition of symbol`   | Defined in multiple `.cpp` files          | Use `inline`, `static`, or move to one source |
| `undefined reference to vtable`   | Missing virtual destructor implementation | Define destructor                             |
| `cannot find -l<library>`         | Library not linked                        | Add `-l` or correct path                      |
| `LNK2005 / LNK1169` (MSVC)        | Multiple definitions                      | Use include guards                            |

<br><br>

Runtime Errors (Crashes & Exceptions)

| Error                                | Cause                 | How to Fix                      |
| ------------------------------------ | --------------------- | ------------------------------- |
| Segmentation fault                   | Invalid memory access | Check pointers & bounds         |
| Stack overflow                       | Infinite recursion    | Add base case                   |
| `std::bad_alloc`                     | Memory exhausted      | Reduce allocation / check leaks |
| Division by zero                     | Zero denominator      | Validate before dividing        |
| `terminate called without exception` | Uncaught exception    | Use try-catch                   |
| Access violation                     | Dangling pointer      | Ensure object lifetime          |

<br><br>

Memory Management Errors

| Error                 | Cause                       | How to Fix                 |
| --------------------- | --------------------------- | -------------------------- |
| Memory leak           | `new` without `delete`      | Use RAII / smart pointers  |
| Double delete         | Deleting same pointer twice | Set pointer to `nullptr`   |
| Dangling pointer      | Object deleted too early    | Manage ownership properly  |
| Buffer overflow       | Out-of-bounds access        | Use `std::vector`          |
| Use-after-free        | Access after delete         | Avoid raw pointers         |
| Mismatched new/delete | `new[]` with `delete`       | Match `new[]` → `delete[]` |

<br><br>

Logic Errors (Compiles but Wrong Result)

| Error                        | Cause                            | How to Fix               |
| ---------------------------- | -------------------------------- | ------------------------ |
| Infinite loop                | Condition never changes          | Fix loop condition       |
| Off-by-one error             | Wrong index limits               | Use `< size()`           |
| Wrong operator (`=` vs `==`) | Assignment instead of comparison | Use `==`                 |
| Uninitialized variable       | No initial value                 | Initialize immediately   |
| Wrong precedence             | Missing parentheses              | Add explicit parentheses |
| Floating-point comparison    | Precision issues                 | Use epsilon comparison   |

<br><br>

STL & Container Mistakes

| Error                             | Cause                    | How to Fix                 |
| --------------------------------- | ------------------------ | -------------------------- |
| Iterator invalidation             | Modifying container      | Re-fetch iterator          |
| Access out of range               | Using `[]` unsafely      | Use `.at()`                |
| Using erased iterator             | Iterator no longer valid | Update iterator            |
| Copying large objects             | Pass-by-value            | Use `const &`              |
| Forgetting `#include <algorithm>` | Missing header           | Include correct STL header |
| `unordered_map::operator[]` fails | Value type not default-constructible | Use `emplace`, `try_emplace`, or `insert` |


<br><br>

Object-Oriented Programming Errors

| Error                           | Cause                              | How to Fix              |
| ------------------------------- | ---------------------------------- | ----------------------- |
| Missing virtual destructor      | Base class deleted polymorphically | Add `virtual ~Base()`   |
| Object slicing                  | Passing object by value            | Use references/pointers |
| Not overriding virtual function | Signature mismatch                 | Use `override`          |
| Calling virtual in constructor  | Undefined behavior                 | Avoid virtual calls     |
| Shallow copy                    | Raw pointers in class              | Implement Rule of 3/5   |


<br><br>

Modern C++ (C++11+) Pitfalls

| Error                            | Cause              | How to Fix            |
| -------------------------------- | ------------------ | --------------------- |
| Dangling reference from `auto&`  | Temporary binding  | Use `auto`            |
| Misusing `std::move`             | Moving too early   | Move only when done   |
| Capturing by reference in lambda | Object destroyed   | Capture by value      |
| Forgetting `constexpr`           | Runtime evaluation | Use `constexpr`       |
| Using raw pointers               | Manual lifetime    | Prefer smart pointers |


<br><br>

Header & Include Errors

| Error                  | Cause                | How to Fix               |
| ---------------------- | -------------------- | ------------------------ |
| Circular dependency    | Mutual includes      | Use forward declarations |
| Missing include guards | Multiple inclusion   | Use `#pragma once`       |
| Including `.cpp` files | Bad practice         | Include headers only     |
| Wrong include order    | Missing dependencies | Include headers first    |

<br><br>

Debugging & Build Configuration Errors

| Error                            | Cause                          | How to Fix             |
| -------------------------------- | ------------------------------ | ---------------------- |
| Works in Debug, fails in Release | UB exposed                     | Fix undefined behavior |
| Optimizer breaks code            | Invalid assumptions            | Remove UB              |
| Different behavior on OS         | Platform-specific code         | Use standard APIs      |
| Undefined behavior               | Uninitialized / invalid access | Use sanitizers         |

<br><br>

Best Tools to Catch These Early

| Tool                       | Purpose           |
| -------------------------- | ----------------- |
| `-Wall -Wextra -Werror`    | Compiler warnings |
| AddressSanitizer           | Memory errors     |
| UndefinedBehaviorSanitizer | UB detection      |
| Valgrind                   | Memory leaks      |
| clang-tidy                 | Static analysis   |
| cppcheck                   | Code quality      |


<br><br>

---




