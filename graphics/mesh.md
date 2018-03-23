# Wireframe Mesh

Shape is defined by the edges that connect points on the surface.

Flow to make wireframe mesh:
1. add box
2. add edge
3. add point
4. draw lines
5. draw line

# Polygon Mesh

Shape is defined by the polygons that connect points on the surface C.
(triangles)

## Polygon Matrix

Edge Matrix:
```
[P0P1, P1P2, P2P0, ...]
```

Polygon Matrix:
```
[P0P1P2, P2P3P4]
 |_T0_|  |_T1_|
```

Flow to create Polygon Mesh:

1. add box
2. add polygon
3. add point
4. draw polygons
5. draw line

Points must be added counter-clockwise.
