# 10/03 Aim: Make it so

## Separate compiliation

You can combine multiple c files into a c program by including them
all in one gcc command.

ex.
```
gcc test.c string.c foo.c woohoo.c
```

You cannot have duplicate function or global vairable names
across these files.

There must be a main function in order to create an executable program.

## `gcc -c`

Will compile a c file into a .o file, it is not a fully
functional program, but it is compiled code. Do this to
compile a .c file that does not contain a main() function.

`.o` files can be linked together with .c files through gcc

## Make
Create compiling instructions and setup dependencies

Standard name for the file is `makefile`

syntax:
```
<TARGET>: <DEPENDENCIES>
	<RULES>
```

EXAMPLE

```
all: dwstring.o main.o
	gcc -o strtest dwstring.o main.o

dwstring.o: dwstring.c dwstring.h
	gcc -c dwstring.c

main.o: main.c dwstring.h
	gcc -c main.c
```

Good idea to make the first command not a filename.
Otherwise won't run it if file hasn't changed.

Calling `make <TARGET>` will run just that target.

### Common Targets:

```
all: DEPENDENCIES
	INSTRUCTION`

run: all
	./executable_file

clean:
	rm executable_file
```
