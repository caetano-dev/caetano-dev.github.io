+++
title = "Programming language concepts"
date = "2023-10-03T12:30:10-03:00"
author = "Pedro Caetano"
tags = ["programming languages"]
keywords = ["programming languages"]
description = "A summary of how programming languages are structured and their different types."
showFullContent = false
readingTime = true
hideComments = false
+++

This is a summary I have written for a college exam and thought it would be cool to share it here.

---

## Language Levels

### High Level

High-level languages are designed to provide programmers with a convenient development environment and control abstractions that make it easier to create programs. They have several advantages, such as:

**Benefits:**

- **Ease of Reading and Learning:** The syntax of high-level languages is designed to resemble human language, making the code more readable and accessible to beginners and experienced programmers.
- **Productivity:** These languages offer high-level constructs, such as control structures and predefined functions, that allow programmers to write code faster.
- **Portability:** Generally, code written in a high-level language can be easily ported to different platforms as most of the hardware complexity is abstracted.
- **Simplified Maintenance:** The readability and organized structure of high-level code makes maintenance and error identification easier.
- **Global Optimizations:** High-level language compilers and interpreters can perform global optimizations, improving the efficiency of the generated code.

**Disadvantages:**

- **Performance:** Compared to low-level languages, high-level languages may have slightly lower performance since the abstraction layer adds overhead.
- **Executable Size:** Programs created in high-level languages can generate larger executables than those written in low-level languages, due to the inclusion of high-level libraries and structures.

### Low Level

Low-level languages operate closer to the hardware and give programmers more direct control over the machine. However, they also present significant challenges.

**Benefits:**

- **Full Control:** Programmers have direct control over memory and hardware resources, allowing for specific optimizations and precise manipulation.
- **Performance:** Low-level languages generally produce highly efficient code, making them ideal for systems that require maximum speed.
- **Lower Overhead:** Code generated in low-level languages tends to have lower overhead compared to high-level languages.

**Disadvantages:**

- **Learning Curve:** Programming in low-level languages can be complex and require in-depth knowledge of the hardware, resulting in a steep learning curve.
- **Error Prone:** Direct control over memory and resources increases the chance of errors such as memory leaks and access violations.
- **Limited Portability:** Code written in low-level languages can be highly dependent on the hardware architecture, which makes portability difficult.
- **Slower Development:** Due to the need to deal with low-level details, software development in low-level languages can take longer.

---

## Syntax x Semantics

Syntax concerns the symbols and forms used in a programming language, while semantics deals with the logic and execution of a program.

Programming languages can have different syntax and maintain the same semantics and vice versa.

### Example:

**Same syntax, but different semantics.**

In Python2:
```python
>>> 1/2
0
```

In Python3:
```python
>>> 1/2
0.5
```

**Same semantics, but different syntax.**

In Moon:
```lua
>> list = {1,2,3}
>> print(#list)
3
```

In Python:
```python
>>> list = [1,2,3]
>>> print(len(list))
3
```

---

## Expressiveness

Language A is strictly more expressive than language B if both of the following statements are true:

1. Any program written in language B can be rewritten in language A, keeping the essential structure of the program intact.
2. Some programs written in language A need to be violently restructured so that they can be written in language B.

---

## Variables and Binding

Variables allow us to store and manipulate data.

### Variable Declaration

When a variable is declared, the computer allocates memory space and defines a name for the variable.

### Assignment

Once a variable is declared, you can assign a value to it. This is the process of binding the variable to a specific data value. The value can be of various types such as numbers, strings or complex data structures such as arrays or objects.

### Dynamic Typing vs. Static Typing

Languages can be categorized into those with dynamic typing and those with static typing.

**Dynamic Typing**

In dynamically typed languages, the type of a variable is determined at runtime, which allows flexibility but can lead to runtime errors.

**Static Typing**

In statically typed languages, the type of the variable must be declared at compile time, offering automatic detection of errors, but with stricter rules.

### Strong Typing vs. Weak Typing

In addition to the distinction between dynamic and static typing, programming languages can also be classified based on typing strength. Strong typing and weak typing are concepts related to the rigidity of type conversion rules in a language.

**Strong Typing**

In strongly typed programming languages, conversions between data types are strictly regulated and limited. This means that operations involving different types require that the types be compatible according to well-defined rules. Any attempt to perform an operation between incompatible types will result in an error.

*Example in Python (strong typing):*

```python
a = 5
b = "10"

# This operation will result in an error as int and str are not compatible
c = a + b
```

In this example, trying to add an integer (`a`) to a string (`b`) causes a type error, because strong typing does not allow this implicit conversion.

**Weak Typing**

In weakly typed programming languages, conversions between data types are more flexible. Operations between different types can be performed with fewer restrictions, and in some cases type conversions are done automatically by the system, even though this can lead to unexpected results.

*Example in JavaScript (weak typing):*

```javascript
var a = 5;
var b = "10";

// JavaScript allows string and number concatenation without error
var c = a + b; // The result will be the string "510"
```

In this example, in JavaScript (a weakly typed language), adding a number (`a`) to a string (`b`) results in the concatenation of the values, as weak typing allows this implicit conversion.

### Contrast with Dynamic and Static Typing

It is important to note that strong typing and weak typing relate to the way languages handle type coercion during program execution, while dynamic and static typing relate to the way types are checked at run or compile time.

| Combination | Description | Example |
|-------------|-------------|---------|
| **Strong typing with static typing** | Requires that types are compatible, and these checks are performed at compile time. | Java |
| **Strong typing with dynamic typing** | Requires types to be compatible, but these checks are performed at runtime. | Python |
| **Weak typing with static typing** | Allows more flexible conversions, but still requires type declaration at compile time. | C |
| **Weak typing with dynamic typing** | Allows flexible conversions and runtime checks. | JavaScript |

The choice between strong and weak typing, along with dynamic or static typing, affects the way type errors are handled, the flexibility of the code, and the ease of development, and is one of the important aspects to consider when choosing a programming language for a specific project.

### Variable Scope

#### Local vs. Global Variables

Variables can have different scopes, which determine where in the code they can be accessed:

- **Local variables:** They are limited to a specific block or function and can only be accessed within that scope. They generally have a shorter lifespan and are destroyed when the block is closed.
- **Global variables:** They have a broader scope and can be accessed from anywhere in the code. They are usually declared outside of functions and have a longer useful life.

### Variable Binding

#### Passing by Value vs. Pass by Reference

In some programming languages, variables are bound to values, while in others, they are bound to references. This difference affects how data is handled:

- **Pass by value:** When a variable is bound to a value, changing the value of the variable does not affect other variables with the same initial value.
- **Pass by reference:** When a variable is bound to a reference, it points to the same memory location as the original variable. Changes made to one variable affect all variables that reference the same data.

#### Immutable Variables

With immutable variables, once a value is assigned to a variable, it cannot be changed. Instead, any modification creates a new variable with the updated value. This helps avoid unintended side effects and increases code predictability.

---

## Stages of Program Execution

### 1. Language Design Time

**Goal:** Language design time is the initial phase in which the programming language itself is conceived and developed. During this stage, language designers and architects create the syntax, semantics, and features of a new programming language. The aim is to create a language that is expressive, efficient and suitable for a specific range of languages.

**Activities:**
- Define the grammar and syntax of the language.
- Design data structures and control flow mechanisms.
- Specification of rules for variable declarations, scope and binding.
- Determine the language's type system and memory management policies.
- Establishment of the standard library and language APIs.

### 2. Implementation Time

**Goal:** Implementation time involves actually writing code in the chosen programming language to create a software application. This phase focuses on transforming a conceptual design into a working program that can run on a computer.

**Activities:**
- Write the source code using the syntax and features of the language.
- Development of algorithms and data structures to solve specific problems.
- Test and debug code to identify and fix errors.
- Profiling and optimizing code to improve performance.
- Integration of third-party libraries and dependencies as needed.

### 3. Preprocessing

**Goal:** The preprocessing phase is optional and mainly applies to languages such as C and C++. It involves manipulating the source code before compilation to prepare it for translation into machine code.

**Activities:**
- Inclusion of header files and macro expansion.
- Conditional compilation based on preprocessor directives.
- Removing comments and white spaces.
- Code generation for specific language features.

### 4. Compilation

**Goal:** Compilation translates the source code into an intermediate representation or machine code that can be executed by the computer's processor. The result is typically a binary or bytecode executable, depending on the language.

**Activities:**
- **Lexical analysis:** Tokenization of source code into meaningful units.
- **Syntax analysis:** Parse tokens to form a syntax tree or intermediate representation.
- **Semantic analysis:** Checking for type, scope and correction errors.
- **Code generation:** Production of machine code or bytecode from the intermediate representation.

### 5. Linking

**Goal:** In languages that support modular programming and separate compilation, the linking phase combines multiple compiled modules (object files) into a single executable program. It resolves references between modules and libraries.

**Activities:**
- **Symbol resolution:** Association of references to functions and variables with their definitions.
- **Address binding:** Assigning memory addresses to program elements.
- Generation of the final executable file or dynamic libraries.

### 6. Loading

**Goal:** Loading places the executable program in memory, making it ready for execution. This phase allocates memory space, resolves addresses, and prepares the program for execution.

**Activities:**
- Memory allocation for code, data and stack segments.
- Resolution of dynamic binding, if applicable.
- Configuration of program control structures.

### 7. Runtime

**Goal:** The runtime phase covers the actual execution of the program. The program interacts with the operating system, hardware, and external resources to perform its intended tasks.

**Activities:**
- Execute the main function or entry point of the program.
- Handling user input and external data.
- Manage memory, resources and concurrency.
- Performing I/O operations and interfacing with hardware.

---

## Scope

Scope, in programming languages, refers to the part of the program where a variable or identifier can be accessed and used. It defines the rules that determine the visibility and lifetime of variables, functions, and other elements within a program.

### Variable Scope

#### Local Variables

Local variables have a restricted scope to a specific block of code, usually delimited by curly braces (as in functions or conditional structures). This means that they can only be accessed within that block and are destroyed when the block is closed. Local variables are useful for avoiding name conflicts and managing memory efficiently.

```python
def example():
    x = 10  # Local variable
    print(x)

example()
print(x)  # This will result in an error as x is not defined in this scope
```

#### Global Variables

Global variables have a broader scope and can be accessed from anywhere in the code, including functions. They are usually declared outside of functions and have a lifetime throughout the execution of the program. However, excessive use of global variables can make code less readable and more prone to errors.

```python
y = 20  # Global variable

def example():
    print(y)  # It is possible to access the global variable within the function

example()
print(y)  # The global variable y can also be accessed out of the function.
```

#### Scope of Functions

Functions also have their own scope. This means that variables declared inside a function are local to that function and cannot be accessed outside of it unless they are returned. This helps encapsulate behavior and avoid name conflicts between functions.

```python
def greeting():
    message = "Hello world!"  # Variable local to the function
    return message

print(greeting())  # Calling the function and printing its output

# Trying to access message here would result in an error as it is outside the scope of the function
```

#### Nested Scope

In some languages, it is possible to have nested scopes, where one scope is contained within another. This means that variables declared in an inner scope can shadow variables with the same name in outer scopes.

```python
x = 30  # Global variable

def example():
    x = 40  # Variable local to the function, shadows the global variable
    print(x)

example()
print(x)  # The global variable x remains unchanged
```

### Dynamic vs. Static Scope

The way scope is handled can vary between programming languages. Some languages, such as Python, use **static scoping**, where the scope of a variable is determined in the static analysis phase, during code compilation or interpretation. Other languages, such as JavaScript, use **dynamic scoping**, where the scope of a variable is determined at runtime, based on the function call stack.

---

## Memory Management, Stacks and Stack Overflow

Memory management affects a program's efficiency, stability, and security.

### Computer Memory

A computer's memory stores data and instructions for executing programs. This memory is divided into several distinct regions, two of the most important of which are the **stack** and the **heap**.

#### Stack

The stack is a region of memory that stores information about the execution of functions and methods. Each time a function is called, a new "stack frame" is created, which contains information such as local variables, return addresses, and other control data. The stack follows a **last-in, first-out (LIFO)** data structure, which means that the most recently called function is the first to complete.

The stack is generally small in size and has a hard limit. This means that if many functions are nested or if the local memory allocation is large, a stack overflow can occur, which is an error that occurs when the stack exceeds its limit.

#### Heap

The heap is a region of memory used to dynamically allocate data during the execution of a program. Unlike the stack, the heap has no LIFO structure and does not have a fixed limit (other than the physical limit of system memory).

The allocation of memory on the heap is controlled manually by the programmer or by a memory management system. Data allocated to the heap remains there until explicitly freed, which can lead to memory leak issues if the free is not done correctly.

### Stack Overflow

Stack overflow is an error that occurs when the stack exceeds its limit. This usually happens when a function calls itself repeatedly (infinite recursion) or when a program nests many functions, each with a large local memory usage. When a stack overflow occurs, the program usually terminates abruptly.

Preventing stack overflow involves consciously using recursion and controlling stack size. For deep recursions, considering optimizing the algorithm or converting the recursion to an iterative approach may be a solution.

### Memory Management

Memory management is the practice of allocating and freeing memory efficiently and safely during the execution of a program. The operating system plays a key role in memory management, providing essential services such as:

- **Memory Allocation:** The operating system allocates blocks of memory to running programs, including stack and heap allocators.
- **Free Up Memory:** When memory is no longer needed, it must be freed to prevent memory leaks. The operating system manages this release.
- **Memory Protection:** The operating system protects memory to prevent a program from accessing unauthorized memory areas, which can result in segmentation errors.
- **Memory Swap:** When physical memory is exhausted, the operating system can use techniques such as paging or swapping to move data between main memory (RAM) and the hard drive.

---

## Performance Comparison between Programming Languages

Formally stating that one language performs better than another is a complex task, due to the following factors.

### Diversity of Applications

Programming languages are created with varying purposes and usage scenarios in mind. Some languages are optimized for specific tasks, such as text manipulation (Python), signal processing (MATLAB), or web development (JavaScript). Therefore, the performance of a language can vary significantly depending on the context in which it is used.

### Varied Implementations

Each programming language has multiple implementations, often developed by different groups and organizations. For example, Python has implementations like CPython, Jython and IronPython. Each of these implementations may have different features and optimizations, which affect performance. Therefore, it is difficult to generalize the performance of "Python" as a whole.

### Compiler and Interpreter Optimizations

The efficiency of a language also depends on the optimizations performed by the compiler (in compiled languages) or the interpreter (in interpreted languages). The quality of these optimizations varies from one implementation to another and can substantially affect performance.

### Algorithm Dependency

The performance of a program largely depends on the algorithms and data structures used. Choosing the right algorithm can have a much greater impact on performance than choosing the language. Two programs written in the same language can have drastically different performance due to the efficiency of the algorithms used.

---

## Interpreted Languages vs. Compiled

Programming languages can be divided into two main categories: interpreted languages and compiled languages.

### Compiled Languages

**What are Compiled Languages?**

In compiled languages, source code written by the programmer is translated by a compiler into machine code or intermediate code that is executed directly by hardware. This means that, before the program is executed, all the code is translated and transformed into a form that can be directly executed by the computer.

**Advantages of Compiled Languages:**

- **Performance:** Generally, compiled programs tend to have higher performance since the code is optimized during compilation.
- **Compile-Time Error Detection:** Syntax and type errors are caught during compilation, which helps to avoid many run-time errors.
- **Efficient Execution:** The compiled code is executed directly by the hardware, without the overhead of an interpreter, making it more efficient in terms of using system resources.
- **Source Code Protection:** Because source code is not required for execution, compiled programs are often more difficult to revert to their original form, which can increase security.

**Disadvantages of Compiled Languages:**

- **Slower Development:** The need to compile the code before execution can increase development time.
- **Lack of Portability:** Compiled code is often platform-specific, which can make portability to different systems difficult.

### Interpreted Languages

**What are Interpreted Languages?**

In interpreted languages, source code is executed directly by an interpreter, line by line. The interpreter translates and executes the code in real time, rather than generating a separate executable program.

**Advantages of Interpreted Languages:**

- **Rapid Development:** Direct execution of the source code simplifies the development process as there is no need to wait for compilation.
- **Portability:** Generally, interpreted programs are more portable, as the interpreter can be implemented on multiple platforms.
- **Ease of Debugging:** The interpreter can provide more informative error messages during execution, making debugging easier.
- **Flexibility:** Real-time execution allows introspection, that is, the ability to inspect and modify the code itself during execution.

**Disadvantages of Interpreted Languages:**

- **Relative Performance:** Interpreted programs generally have lower performance compared to compiled programs due to interpreter overhead.
- **Lack of Source Code Protection:** Because source code is necessary for execution, interpreted programs may be more susceptible to reverse engineering and unauthorized appropriation.
- **Less Detection of Errors at Compile Time:** Syntax and type errors are only detected during execution, which can lead to runtime errors.