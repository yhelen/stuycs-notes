# 10/10 Aim: If you don't pay attention you'll get into a heap of trouble!

## Stack memory vs Heap memory
Computer programs separate memory usage into two parts: stack and heap.

Every program can have its own stack and heap.

## Stack memory
Stores all normally delcared variables (including pointers and structs),
arrays and function calls

Functions are pushed onto the stack in the order they are called, and
popped off when completed.

When a function is popped off the stack, the stack memory associated
with it is released.

## Heap Memory
Stores dynamically allocated memory.

Data will remain in the heap until it is released.
(or the program terminates).

Can be accessed through pointers.

Can be accessed across many functions.

# 10/12 Aim: malloc & free: The dynamic duo!

## Dynamic Memory Allocation

### `malloc(size_t size)`

Allocates x bytes of memory (From the heap)

Returns the address at the beginning of the allocation

Returns a `void *`, always typecast to the correct pointer type!!

```c
int *p;
p = (int *) malloc(5 * sizeof(int));
```

### `free(void *ptr)`
Releases dynamically allocated memory.

Takes one paramater, a pointer to the beginning of a
dynamically allocated block of memory.

Every call to malloc/calloc should have a corresponding call to free.

Only frees if it is the original pointer. Otherwise, segfaults.

```c
int *p;
p = (int *)malloc(20);
free(p)
```

### `calloc(size_t n, size_t x)`
Allocates `n * x` bytes of memory

Ensures that each bit is set to 0

Works like `malloc` in all other ways

```c
int *p;
p = (int *) calloc(5, sizeof(int));
```

### `realloc(void *p, size_t x)`
Changes the amount of memory allocated to a given block.

`p` must be a pointer to the beginning of an allocated block of memory,
but it does not have to be the original pointer.

If `x` is smaller than the oriinal size of allocation, the extra bytes
will be released.

If `x` is larger, it will extend the memory OR reassign and copy the
information.

```c
int *p;
p = (int *)malloc(20);
p = (int *)realloc(p, 40);
```
