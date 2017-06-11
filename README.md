# Embedded C Style

*Coding standards and guidelines for embedded systems written in C.*

## Table of Contents

  1. [Header Files](#header-files)
  1. [Scoping](#scoping)
  1. [Functions](#functions)
  1. [Naming](#naming)
  
## Header Files

  <a name="header-files"></a><a name="1.1"></a>
  - [1.1](header-files--gap) **Generally accepted practices**: 
  
    This guide adopts the [Header Files](https://google.github.io/styleguide/cppguide.html#Header_Files) section of the [Google C++ StyleGuide](https://google.github.io/styleguide/cppguide.html) in its entirety.
    
  <a name="1.2"></a>
  - [1.2](header-files--prototypes) **prototypes**: Use prototypes when declaring functions.
  
    Prototypes allow the compiler to detect more errors at compile time.
    
  <a name="1.3"></a>
  - [1.3](header-files--public-interface) **public interface**: The header file is the public interface to a module.
  
    A header file should contain only the constants and data structures need by the modules which use the header file. Constants and data structures which are part of the internal implementation of the module should reside in the module's *.c* file.
    
  <a name="1.4"></a>
  - [1.3](header-files--no-args) **functions with no arguments**: Use *void* to indicate that a function takes no arguments.
  
    Bad:
    
    ```cpp
    int foo();
    ```
    
    Good:
    
    ```cpp
    int foo(void);
    ```
    
    Yes, in C++ the *void* is not required.
  
## Scoping

  <a name="scoping"></a><a name="2.1"></a>
  - [2.1](scoping-struct)
  

