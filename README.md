# Embedded C Style

*Coding standards and guidelines for embedded systems written in C.*

## Table of Contents

  1. [Modules](#modules)
  1. [Header Files](#header-files)
  1. [Limited Resources](#limited-resources)
  1. [Interrupt Service Routines](#isrs)
  1. [Scoping](#scoping)
  1. [Functions](#functions)
  1. [Naming](#naming)
  1. [Formatting](#formatting)
  
## Program Structure
  <a name="header-files"></a><a name="1.1"></a>
  - [1.1](program-structure--modules) **Modules**: Organize the code into modules.
  
    A *module* is a collection of closely related functions, data structures
    and data.
  
  - [1.2](program-structure--files) **Module Structure**: A module comprises two files: a header and an implementation.
  
    The header file has the extension *.h*; the implementation file carries the *.c* extension.
    
  - [1.3](prefer-function-interface) **Prefer a functional module interface**: If a module carries state (static variables), use a function to access and modify that state.
  
    Bad:
    ```cpp
      export int value = 0;
    ```
    
    Good:
    ```cpp
      static int value = 0;
      int getValue(void) {
        return value;
      }
      void setValue(int _value) {
        value = _value;
      }
    ```
    
  - [1.4](prefer-stateless-modules) **Prefer stateless modules**: Whenever possible, avoid storing state in modules.
  
    The preferred way to manage state is declare a local variable or struct and pass it as an argument to called functions.
    
    Doing so give data a definite lifetime: the lifetime of the containing function. It also manages the visibility of the data to other modules and makes it simpler to reason about who might be modifying it.
    
    If the state is large, memory can be allocated for from the heap.
  
  - [1.4](prefer-pure-functions) **Prefer functions with no side effects**: Whenever possible, organize the code as functions that use only their arguments as inputs and which return a value, without other side effects.
    
    Side effects include i/o operations and modifying static variables. Pure (side-effect free) functions are easy to unit test and easy to reason about.
  
  - [1.4](object-based-programming) **Object-like Programming**: Use an object-like style only when necessary.
  
    If an object-oriented style fits some part of the program logic, especially if multiple instances are needed, then an object-based style may be considered.
    
    A single module represents that would be the *class* in an object-oriented language. A *struct* in the header file holds the state of an instance.  Function rototypes in the header file represent methods. Functions local to the *.c* file represent private methods.
    
    The convention is to pass a pointer to the instance's state as the first argument of the functions.
    
    Note: It is possible to implement features like polymorphism by storing pointers to functions in the *struct* that holds the instance state. If this is truly needed, use C++ rather than C.

## Header Files

  <a name="header-files"></a><a name="1.1"></a>
  - [2.1](header-files--gap) **Generally accepted practices**: 
  
    This guide adopts the [Header Files](https://google.github.io/styleguide/cppguide.html#Header_Files) section of the [Google C++ StyleGuide](https://google.github.io/styleguide/cppguide.html) in its entirety.
    
  <a name="1.2"></a>
  - [2.2](header-files--prototypes) **Prototypes**: Use prototypes when declaring functions.
  
    Prototypes allow the compiler to detect more errors at compile time.
    
  <a name="1.3"></a>
  - [2.3](header-files--public-interface) **Public interface**: The header file is the public interface to a module.
  
    A header file should contain only the constants and data structures need by the modules which use the header file. Constants and data structures which are part of the internal implementation of the module should reside in the module's *.c* file.
    
  <a name="1.4"></a>
  - [2.3](header-files--no-args) **Functions with no arguments**: Use *void* to indicate that a function takes no arguments.
  
    Bad:
    
    ```cpp
    int foo();
    ```
    
    Good:
    
    ```cpp
    int foo(void);
    ```
    
    Aside to C++ experts: yes, in C++ the *void* is not required.
  
## Limited Resources

  <a name="limited-resources"></a>

  The governing philosopy of this guide favors human readability and ease of
  comprehension over every consideration other than meeting the functional
  specification. Modular maintainability is preferred even at the cost of extra
  memory or CPU cycles, again, so long as functional requirements are met.

  Working in very constrained environments, such as 8-bit
  microcontrollers, doesn't require an abandonment of style, as most of this
  guidance costs nothing at runtime. The principal exception is functions,
  which present a speed/space tradeoff.

  The primary appeal of functions is saving space at the cost of CPU
  cycles. A relatively large function called in more than one place is
  generally a good thing, unless there's not enough CPU cycles available to
  cover the function call overhead.

  Very small functions, such as getters and setters, are likely to be both
  larger and slower than a non-functional interface.

  While many designers respond to this situation by using macros or even
  dissolving program structure entirely, this guide recommends the use of
  [`inline extern`](https://gcc.gnu.org/onlinedocs/gcc/Inline.html).

  <a name="3.1"></a>
  - [3.1](limited-resources--inline) **Inline functions**: Prefer `inlne
  extern` functions to macros.
  
  <a name="3.2"></a>
  - [3.2](limited-resources--macros) **Macro arguments**: Always put
  parenthesis around the formal parameters of macros.

## Interrupt Service Routines

  <a name="isrs"></a><a name="4.1"></a>
  - [4.1](isrs--simple) **Simple:** Prefer simpler ISR structures

  Interrupts, being asynchronous, are difficult test comprehensively and even
  more difficult to debug. 

  - [4.2](isrs--short) **Quick:** Return from the ISR as soon as practical


<!---
## Scoping

  <a name="scoping"></a><a name="4.1"></a>
  - [5.1](scoping-struct)
-->
  

## Functions

  <a name="functions"></a>
  This guide adopts the [Functions](https://google.github.io/styleguide/cppguide.html#Functions) section of the Google C++ Style Guide.
    
## Naming

  <a name="naming"></a>
  This guide adopts the [Naming](https://google.github.io/styleguide/cppguide.html#Naming) section of the Google C++ Style Guide.
    
## Formatting

  <a name="formatting"></a>
  
  This guide adopts the [Formatting](https://google.github.io/styleguide/cppguide.html#Formatting) section of the Google C++ Style Guide.
  
