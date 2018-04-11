# Backface Culling

Only drawing the polygons that are forward facing

**N**: Surface normal, perpendicular to polygon

**V**: Vector from surface to observer

1. Calculate **N**
    * **N** = **A** x **B**
    * **A** = <P1-P0>
    * **B** = <P2-P0>
2. Find the angle between **N** and **V**
    * **N** * **V** = ||N|| ||V|| cos(theta)
    * **V** = <0, 0, 1> (for now)
3. If the angle is between -90 and 90 (not inclusive), draw
    * cos > 0 in acceptable range
    * Using **V** = <0, 0, 1>, if z-component of **N** is positive, draw it.
