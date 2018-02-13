# Matrices

```
A 3 x n matrix
--                   --
| x0, x1, x2, ..., xn |
| y0, y1, y2, ..., xn |
| z0, z1, z2, ..., zn |
--                   --
```

## Matrix Multiplication

M * N: # of columns in M **MUST** equal the number of rows in N

A x B * B x C = A * C

* Non-commutative

```
          | a |
[1 2 3] * | b | = [1a + 2b + 3c]
          | c |
```

```
| 1 2 3 |   | a b |   | 1a+2c+3e 1b+2d+3f |
| 4 5 6 | * | c d | = | 4a+5c+6e 4b+5d+6f |
| 7 8 9 |   | e f |   | 7a+8c+9e 7b+8d+9f |
```

### Multiplicative Identity Matrix

M * I = M

* Square
* Diagonal of 1s, 0s everywhere else

```
| 1 0 |   | a |   | a |
| 0 1 | * | b | = | b |
```
