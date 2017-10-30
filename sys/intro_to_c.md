# 9/11 Aim: Let's C what you can do

## Basic C code

### Source Code:
- Put in .c files (convention)
- Naming convention: snake_case

### Compiling
- gcc: GNU
    * Compiles to architecture specific (OS + Processor) executable files
    * Default name of compiled file is a.out
    * gcc option: -o <file> compiles to file

---

# 9/12 Aim: Hello, World!

## C
- Developed in early 70s by Dennis Ritchie while working on UNIX
- 1978 - published by Ritchie and Kernighan -> "The C Programming Language"
- Designed to match closely with assembly, making programs lean and fast
- Procedural langauge (NOT OOP)
- Syntax was used as basis for Java

---

# 9/13 Aim: Variables are the spice of life

Commands in c are often explained in sections 2/3 of *man*

C was meant for a time when machines were not as powerful
Unlike Java, C will not include all functions (unlike *import*)

## Including Libraries

To use functions defined in other files, 2 things happen:

1. Check that you are using the function correctly
   That the arguments and returnt ype match the function definition
2. Link the code for the external function to your executable code
   `gcc` can automatically link functions in standard libraries
   Therefore, only containing functions that you use

Warning from *hello.c*
Failure in step 1
Error from linker
Failure in step 2

## `#include`
    * Used to include function headers with your code.
    * Necessary to match arguments and return types (step 1).
    * Not neessary for linking (step 2).
    * Put system libraries inside <>
       - e.g. *#include <stdio.h>*
    * No semicolon after

Standard to include:
* `stdio.h`
* `stdlib.h`
---

# 9/14 Aim: Always read the fine print

## Primitive data types in java
* int
* double
* float
* long
* short
* char
* boolean
* byte

## In C:

lose byte and boolean

## C Primitive Variable Types
* All C primitives are numeric
* The only differences are:
    - floating point vs. integer
    - size of variable in memory
* Size can be platform dependent
    - sizeof(<TYPE>) can be used to find the size in bytes:
        * e.g. sizeof(int)

%% TODO FIX
    Type        Standard size (Bytes)       Range
    char            1                       -128 to 127
    short           2
    int             4                       about -2 billion to 2 billion
    long            8

    float           4                       7 digit precision
    double          8                       14 digit

printf - *stdio.h*
    The most important C function!
    Prints formatted strings
    printf(<string literal>, <var1>, <var2>, ...)

    Simple printf does not need <var> arguments
        e.g. printf("hola")

    printf DOES NOT add a newline at the end

    If you want to print variables, you must include formatting
    placeholders in the string arguement.
        `int`i = 5;
        printf("i is %d", i)

    Type        Formatting Character
    int             %d
    long            %ld
    float           %f
    double          %lf
                    %0.<x>f will provide x digits
                            after the floating point
    char            %c
    char array      %s
    pointer         %p
