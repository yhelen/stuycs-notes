# Transformations

* Translation
* Dilation
* Rotation

These are all affine transformations.

E: edge matrix, T: transformation[ matrix]( matrix)

E * T or T * E? The second, to preserve dimensions.

## Translation

```
(x, y, z) ---T(a,b,c)--> (x + a, y + b, z + c)

| 1 0 0 a |   | x |   | x + a |
| 0 1 0 b |   | y |   | y + b |
| 0 0 1 c | x | z | = | z + c |
| 0 0 0 1 |   | 1 |   |   1   |

    4 x 4  x  4 x N  =  4 x N
```

## Dilation

```
(x, y, z) ---D(a,b,c)--> (ax, by, cz)

| a 0 0 0 |   | x |   | ax |
| 0 b 0 0 |   | y |   | by |
| 0 0 c 0 | x | z | = | cz |
| 0 0 0 1 |   | 1 |   | 1  |
```

## Rotation

```
(x, y, z) ---Rtheta--> (xcos(theta)-ysin(theta), ycos(theta)+xsin(theta), x)
```
