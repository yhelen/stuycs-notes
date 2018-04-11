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
