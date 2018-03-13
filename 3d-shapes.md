# 3D Shapes

## Box

Defining Points: Vertices

Given Information:
* P0 (top left front)
* Width
* Height
* Depth

## Sphere

Defining Points: Points on the surface

Given Information:
* Center
* Radius

Generate the defining points by drawing a circle and rotating it.

* x-axis: poles on the left/right
* y-axis: poles at top/bottom

circle:
```
| 1        0        0  |   | rcos(theta) |   | rcos(theta)         |   x
| 0 cos(phi) -sin(phi) | x | rsin(theta) | = | rsin(theta)cos(phi) | = y
| 0 sin(phi)  cos(phi) |   | rsin(theta) |   | rsin(theta)sin(phi) |   z
```

theta: angle of circle creation
phi: angle of circle rotation
