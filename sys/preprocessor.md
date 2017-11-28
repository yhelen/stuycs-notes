# 11/28 Aim: C, the ultimate hipster, using # decades before it was cool

## `#`

Used to provide preprocessor instructions.

These direcives are handled by `gcc` first.

### `#include <LIBRARY> | "LIBRARY"`

Link libraries to your code.

### `#define <NAME> <VALUE>`

Replace all occurrences of NAME with VALUE

```c
# define TRUE 1
```

#### macros:

```c
#define SQUARE(x) x * x
```

### `#ifndef`

```c
#ifndef <IDENTIFIER>
#define <IDENTIFIER>
<CODE>
#endif
```

If the identifier has been defined, ignore all the code up until the
endif statement.
