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
* z-axis: circle

circle:
```
| 1        0        0  |   | rcos(theta) |   | rcos(theta)         |   x
| 0 cos(phi) -sin(phi) | x | rsin(theta) | = | rsin(theta)cos(phi) | = y
| 0 sin(phi)  cos(phi) |   | rsin(theta) |   | rsin(theta)sin(phi) |   z
```

Should draw semicircle, rotate full circle
INSTEAD OF
drawing circle, rotate semicircle

theta: angle of circle creation (0 to pi)
phi: angle of circle rotation (0 to 2pi)

Pseudocode:
```
for phi: 0 to 2pi:
    for theta: 0 to pi:
        x = rcos(theta) + cx
        y = rsin(theta)cos(phi) + cy
        z = rsin(theta)sin(phi) + cz
```

## Torus

Defining Points: Points on the surface

Given Information:
* R (radius of torus)
* r (radius of circle)
* Center

Generate the defining points by translating a circle and rotating it

* If we move over x, rotate about y
* If we move over y, rotate about x
* If we move about z, no torus possible

Draw a torus (translate x, rotate y)
```
y rotation                      Circle:             Torus
| cosphi  theta sinphi |   | rcos(theta) + R |   | cosphi(rcostheta + R) + cx  |
| 0       1     0      | x | rsin(theta)     | = | rsintheta + cy              |
| -sinphi 0     cosphi |   | phi             |   | -sinphi(rcostheta + R) + cz |
```

