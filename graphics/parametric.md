# Parametric Equations

Define a curve as a system of equations based on an independent variables.

```
x = f(t)
y = g(t)
z = h(t)
```

For consistency, we will use 0 <= t <= 1

General Parametric Framework (pseudocode)
for t: 0 -> 1
* x = f(t)
* y = g(t)
* add (x,y)

Line (x0, y0) -> (x1, y1)
* f(t) = x0 + t(Δx)
* g(t) = y0 + t(Δy)

Circle (xc, yc) r
* f(t) = rcos(2pi(t)) + xc
* g(t) = rsin(2pi(t)) + yc
