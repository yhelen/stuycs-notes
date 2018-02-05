## Bresenham's Line Algorithm

Find the pixels that best approximate a target line.

Assume:
* (x<sub>0</sub>, y<sub>0</sub>) &rarr; (x<sub>1</sub>, y<sub>1</sub>), all ∈ ℤ
* Only lines in octant I. (0 < m < 1)
* x<sub>0</sub> < x<sub>1</sub>

If (x + 1) / (y + 1/2) is above the line, draw the lower pixel.
If (x + 1) / (y + 1/2) is below the line, draw the upper pixel.
If (x + 1) / (x + 1/2) is on the line, draw either. (Pick one)
