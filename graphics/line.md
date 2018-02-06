# Bresenham's Line Algorithm

Find the pixels that best approximate a target line.

Assume:
* (x<sub>0</sub>, y<sub>0</sub>) &rarr; (x<sub>1</sub>, y<sub>1</sub>), all ∈ ℤ
* Only lines in octant I. (0 < m < 1)
* x<sub>0</sub> < x<sub>1</sub>

If (x + 1) / (y + 1/2) is above the line, draw the lower pixel.
If (x + 1) / (y + 1/2) is below the line, draw the upper pixel.
If (x + 1) / (y + 1/2) is on the line, draw either. (Pick one)

### Testing (x + 1, y + 1/2)

```
y = mx + b
0 = mx - y + b  m = Δy / Δx
0 = (Δy / Δx)x - y + b
0 = (Δy)x - (Δx)y + (Δx)b
    A = Δy
    B = -Δx
    C = (Δx)
0 = Ax + By + C
f(x, y) = Ax + By + C
```

f(x, y) = 0 - on the line
f(x, y) < 0 - above the line
f(x, y) > 0 - below the line

## First Draft (x<sub>0</sub>, y<sub>0</sub>) &rarr; (x<sub>1</sub>, y<sub>1</sub>)

```
x = x<sub>0</sub>, y = x<sub>0</sub>
d = f(x + 1, y + 1/2)
while x ≤ x<sub>1</sub>
    plot(x, y)
    x++
    if d > 0
        y++
    d = f(x + 1, y + 1/2)
```

Optimize `d = f(x + 1, y + 1/2)` calculation at the end:
* if x increases by 1, `d = d + A`
* if y increases by 1, `d = d + B`

```
x = x<sub>0</sub>, y = x<sub>0</sub>
d = f(x + 1, y + 1/2)
while x ≤ x<sub>1</sub>
    plot(x, y)
    if d > 0
        y++
        d += B
    x++
    d += A
```

Optimize `d` calculation in beginning

```
d<sub>0</sub> = f(x<sub>0</sub> + 1, y<sub>0</sub> + 1/2)
DISTRIBUTION...
              = Ax<sub>0</sub> + By<sub>0</sub> + C + A + 1/2 B
               |___________________________________|
                                = 0
              = A + 1/2 B
BUT GET RID OF 1/2 -> SCALE BY 2
```

2d = 2A + B
