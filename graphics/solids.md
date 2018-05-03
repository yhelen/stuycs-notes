# Solids

## Scanline Conversion

Filling a polygon by drawing consecutive horizontal (or vertical) lines.

* Need to order vertices vertically, for a bottom (B), middle (M), and top (T).
* Need to find the endpoints of each scanline.
* y starts at bottom y and ends at top
* x0 is on edge BT, starts at bottom x, ends at top x
* x0 += Δ0
* Δ0 = (xT-xB) / (yT-yB)
* x1 is either on BM until y=yM (or x = xM??) then on MT
* x1 += Δ1
* Δ1 = (xM-xB) / (yM - yB) OR Δ1 = (xT - xM) / (yT - yM)

## z-buffer

z-buffer is a 2D array of floating point values that directly corresponds
to the screen.

* Check the z-buffer before updating the screen.
* Initialize each z value to the smallest possible value.

Must modify:
* `Plot()`: Must check/modify z-buffer
* `DrawLine()`: must compute z values
* Scanline conversion must compute z values
