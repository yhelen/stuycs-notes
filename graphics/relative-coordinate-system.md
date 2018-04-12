# Relative Coordinate System

Currently, transformations are applied to all shapes in the polygon/edge
matrix.

In a RCS, we use transformations to modify the world in which we
draw our shapes.

Each shape is drawn in a different world.

## Drawing in an RCS

1. Generate polygons/edges
2. Apply the current coordinate system to these points.
3. Draw the polygons/edges to the image.

## Coordinate System Stack

* We will maintain a stack of coordinate systems.
* The top will always be the most current coordinate system.
* The bottom will always be the identity matrix.
* All transformations modify the top.
* Push will push a copy of the top.

```
Command:    Stack:
push        I
            I
-----------------
move        I * M
            I
-----------------
box         I * M
            I
-----------------
push        I * M
            I * M
            I
-----------------
move        I * M * M
            I * M
            I
-----------------
rotate      I * M * M * R
            I * M
            I
-----------------
sphere      same
-----------------
pop         I * M
            I
```
