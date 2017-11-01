# 9/18 Aim: A vast array of possibilities

## Data Types and Variables

* Character literals are single characters inside ''
    - eg. `'a'`, `'*'`, ...
* String literals exists, even though there is no String data type
    - eg. `"hello"`, `"you smell"`
* The order that identifiers are declared in matters.
    - This includes functions, so they must be declared before use.

Variables cannot be declared inside for loop statements
but they can be initialized.

Any variable type can be declared an "unsigned variable that
the variable will never be negative.
* The lower bound of any unsigned variable is 0
* The upper bound will be greater than the signed version
    - eg. `unsigned char x; // 0 <= x <= 255`

All boolean values are numbers:
* 0 is false. Anything else is true

*MISTAKE:*  
`if(x = 6) {...}  `
NEEDS TO BE `if(x==6)  `

## Memory Management

Memory allocation either happens at compile time or at runtime (dynamic)

### Compiler Allocated Memory

* Packaged with the binary of the program
* There is no standard default value
* Variables and arrays are allocated here.

```c
float a
int b[5]
```

#### Arrays

Must have a fixed size set at declaration as a literal.

There is no length function
* You CAN use the `sizeof()` to find the amount of memory allocated
  to that variable.

There is no boundary checking

Segmentation fault: Program has accessed memory it should not

---

# 9/20 Aim: Try not to hurt yourself, the point is sharp.

## Pointers

Variables designed to store memory addresses
* (array variable is a kind of pointer)

`*` is used to declare a variable as a pointer type

`int *p, double *q, char *r`

(you can put a space after the *)

& is used to get the address of a variable (address of operator)

& is also used as the deference operator
* It accesses the value at the memory location stored in a pointer.

All pointer variable types are the same size.

## Pointer Arithmetic

```c
int *p = &i;
char *c = &i;

p++; // will add 4 to p
c++; // will add 1 to p

arrays work as so:
arr[i] means *(arr+i)
```

---

# 9/25 Aim: How to write functioning code

Seeding a random num generator (usually EPOCH time in other languages by default)

## Arrays and Pointers
Array variables are immutable pointers

Pointers can be assigned to array variables.
```c
    int ray[5];
    int *rp = ray;

    ray[3]; //<==> ?
            //     *(rp + 3)
```

ALSO LEGAL:

```c
    3[ray] = *(3 + ray)
```

`a[i]` notation is shorthand for `*(a + i)`
in fact...

```c
    a[i] <==> *(a + i)
    i[a] <==> *(i + a)
```
