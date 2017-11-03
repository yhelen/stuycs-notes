# 11/3 Aim: Input? fgets about it

## Command Line Arguments:

```c
int main( int argc, char *argv[] )
```

Program name is considered the first command line argument

* `argc`
    - Number of command line arguments
* `argv`
    - Array of command line arguments

## `scanf - <stdio.h>`

```c
scanf( <FORMAT STRING>, <VAR 1>, <VAR 2> ...)
```

Reads in data from `stdin` using the format string to determine types.

Puts the data in each variable (which must be pointers).

eg:
```c
int x; float f; double d;
scanf("%d %f %lf", &x, &f, &d);
```
