# 10/18 Aim: Back to the grind

## Valgrind
Tool for debugging memory issues in C programs

Compile with -g in order to use valgrind (and similar tools)
```
gcc -g foo.c
```

Usage:
```
valgrind --leak-check=yes <program>
```

---
# 10/19 Aim: Get Dem Bugs

`(gdb) run`: run code

`(gdb) list`: list error code line

`(gdb) break 17`: set a breakpoint

`(gdb) run`: run from start to breakpoint

`(gdb) print sum`: print a variable

`(gdb) continue`: continue, run through

## Commands from in the gdb shell
* `run`: runs the program until it ends/crashes
* `list`: show the lines of code run around a crash
* `print <VAR>`: print a variable
* `backtrace`: show the current stack
* `break <line number>`: creates a breakpoint at the given line

### Running a program in pieces
* `continue`: run the program until the next breakpoint
* `next`: run the next line of the program only
* `step`: run the next line of the program, if that is a function
  call, run only the next line of that function
