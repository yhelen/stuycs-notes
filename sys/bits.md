# 10/23 Aim: A bit of wisdom

"%o" & "%x" are printf formatting characters that work on integer types.
What do they do?

## binary, octal, and hexadecimal integers
Other base formatting characters:
* %o - octal
* %x - hexadecimal

You can define native integers in bases 2, 8, and 16 by using
the following prefixes.
* 0b : binary
* 0 : octal
* 0x : hexadecimal

*THIS DOES NOT CHANGE THE VALUE*: 0b1011 = 013 = 0xB = 11

## bitwise operators
Evaluated on each individual bit of a value.

#### >> right shift (ex. x >> 1)
Move all bits to the right, add 0s in the front

```c
char b = 0b1011;
b >> 1;
// 00001011 becomes 00000101
```

#### left shift (ex. x << 1)
Move all bits to the left, add 0s in the end

```c
char b = 0b1011;
b << 1;
// 00001011 becomes 000110110
```

Left shift and Right shift will not overfow end bits into ajacent memory.

#### ~ negation (ex: ~x)
Flip every bit

#### | or (ex. a | b)
Perform or for each pair of bits in (a, b)

#### & and (ex. a & b)
Perform and for each pair of bits in (a, b)

#### ^ xor (ex. a ^ b)
Perform xor for each pair of bits[ ]( )in (a, b)

xor swap:
1) a = a ^ b;
2) b = a ^ b;
3) a = a ^ b;
