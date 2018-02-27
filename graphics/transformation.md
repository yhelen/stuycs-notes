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

### Rotating about z-axis

```
(x, y, z) ---Rtheta--> (xcos(theta)-ysin(theta), ycos(theta)+xsin(theta), z)
| cos(theta) -sin(theta) 0 0 |   | x |   | xcos(theta) - ysin(theta) |
| sin(theta)  cos(theta) 0 0 |   | y |   | ycos(theta) + xsin(theta) |
| 0           0          1 0 | x | z | = |             z             |
| 0           0          0 1 |   | 1 |   |             1             |
```

### Rotating about x-axis

```
(x, y, z) ---Rtheta--> (x, ycos(theta)-zsin(theta), zcos(theta)+ysin(theta))
```

### Rotating about y-axis

```
(x, y, z) ---Rtheta--> (xcos(theta)+zsin(theta), y, zcos(theta)-xsin(theta))
```

## Combining Transformations

* E<sub>0</sub>: Edges
* T: Translation
* R: Rotate
* S: Scale

* T * E<sub>0</sub> = E<sub>1</sub>
* R * E<sub>1</sub> = E<sub>2</sub>
* S * E<sub>2</sub> = E<sub>3</sub>
* E<sub>3</sub> = S * E<sub>2</sub>
* E<sub>2</sub> = R * E<sub>1</sub>
* E<sub>1</sub> = T * E<sub>0</sub>
* E<sub>3</sub> = (S * R * T) * E<sub>0</sub>
