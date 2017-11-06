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

# 11/6 Aim: Are your processes running? Then you should catch them!

## `fgets - <stdio.h>`

Read in from a file stream and store it in a string.

```c
fgets( <DESTINATION>, <BYTES>, <FILE POINTER> );

fgets( s, n, f );
```

Reads at most n-1 characters from filestream f and stores it in s.

* File pointer:
    - `FILE *` type, more complex than a file descriptor
    - `stdin` is a `FILE *` variable

Stops at newline, end of file, or byte limit.

If applicable, keeps the newline character as part of the string,
appends `NULL` after.

```c
fgets(s, 256, stdin)
```

read a line of text from standard in

## `sscanf - <stdio.h>`

Scan a string and extract values based on a format string.

```c
sscanf(<SOURCE STRING>, <FORMAT STRING>, <VAR 1>, <VAR 2, ...);
```
