# 10/06 Aim: Finding your type

## `typedef`
Provide a new name for an existing data type

```c
typedef <real type> <new name>;
ex:
    typedef unsigned long size_t;
    size_t x = 139; // x is really an unsigned long
```

### IMPORTANT
The use of typedef is another in a long line of
religious wars in programming (see emacs v vim,
tabs v spaces, etc.)

## Struct
Create a new type that is a collection of values.

```c
struct { int a; char x; } s;
```

type is `struct { int a; char x }`

Easier to store as powers of two (struct above is 5 bytes, but uses 8 bytes)

```c
struct foo { int a; char x; };
```

Here, foo is a prototype for this kind of struct,
to be used later, as such:

```c
struct foo s;
```

A variable can be created at the same time as a prototype,
but is generally unadvised.

```c
struct foo {
    int a;
    char x;
};
```

is the advised declaration.

---

# 10/10 Aim: If you don't pay attention you'll get into a heap of trouble!

## Struct

```c
struct foo { int a; char x; } s;
```

We use the `.` operator to access a value inside a struct

```c
s.a = 10;
s.x = '@';
```

`.` binds before `*`

```c
p = &s;
(*p).x;
```

To access data from a struct pointer you can also use `->k`:

```c
p->x; //this is the same as (*p).x
```
