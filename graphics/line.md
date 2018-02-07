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
x = x0, y = x0
d = f(x + 1, y + 1/2)
while x ≤ x1
    plot(x, y)
    if d > 0
        y++
        d += B
    x++
    d += A
```

Optimize `d` calculation in beginning

```
d0 = f(x0 + 1, y0 + 1/2)
DISTRIBUTION...
              = Ax0 + By0 + C + A + 1/2 B
               |___________________________________|
                                = 0
              = A + 1/2 B
BUT GET RID OF 1/2 -> SCALE BY 2

2d = 2A + B
```

```
x = x0, y = x0
d = 2A + B
while x ≤ x1
    plot(x, y)
    if d > 0
        y++
        d += 2B
    x++
    d += 2A
```

## Octant II?

Possible:
* (x, y + 1)
* (x + 1, y + 1)

Changes from Octant I:
* Change `x ≤ x1` to `y ≤ y1`
* Switch `x++` `y++` blocks
* initial changes to `d0 = f(x0 + 1/2, y0 + 1)`, which equals A + 2B
* if `d < 0` increment x

## Octant VIII?

Possible:
* (x + 1, y)
* (X + 1, y - 1)

Changes from Octant I:
* `d0 = 2A - B`
