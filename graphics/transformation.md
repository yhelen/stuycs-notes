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
