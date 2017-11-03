# 9/25 Aim: How to write functioning code

p++ (return then increment)
++p (increment then return)

## Writing Functions
function headers:

```
<return type> <name> (<parameters>)
```

* All functions are pass by value
    - Functions arguments are new variables that contain a copy of the
    data passed to them.

```c
double a = 2.3;
foo(a);

void foo(double x) {
    x = 19;
}

// `a` will still be 2.3


double a[5];
foo(a);
void foo(double *x)
    x[0] = 23;
// MODIFIES THE ORIGINAL ARRAY
```

---

# 9/26 Aim: Let's Head to Function Town

Writing a function with a function being passed in: you really pass a pointer
to the array not a copy of the array

You can declare a function header before use OR in a `.h` file:

```c
void fxn_name(int *, char);
```

If using a `.h` file, remember to include:

```c
#include "header_name.h"
```

You must declare a function before you use it. Done in few ways:
1. Write the entire function at the top of your code. Make sure your order is correct!
2. Write function headers at the top, then define later.
3. Put all function headers in another file (`.h`). Then include and provide
   definitions there.
