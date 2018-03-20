# Splines

Curves that can be combined smoothly.

for t: 0-1, t += step
* x = a<sub>x</sub>t<sup>3</sup>+b<sub>x</sub>t<sup>2</sup>+c<sub>x</sub>t+<sub>d</sub>
* y = a<sub>y</sub>t<sup>3</sup>+b<sub>y</sub>t<sup>2</sup>+c<sub>y</sub>t+<sub>d</sub>

## Hermite Curves

Given Information:
* P0, P1: Endpoints
* R0, R1: Rates of change at endpoints
* f(t) = a<sub>x</sub>t<sup>3</sup>+b<sub>x</sub>t<sup>2</sup>+c<sub>x</sub>t+<sub>d</sub>: Points on curve
* f'(t) = 3a<sub>x</sub>t<sup>2</sup>+2b<sub>x</sub>t+c: Rates of change

* When t=0 f(t) = d: P0
* When t=0 f'(t) = c: R0
* When t=1 f(t) = a + b + c + d: P1
* When t=1 f'(t) = 3a + 2b + c: R1

```
| 0 0 0 1 |   | a |   | P0 |
| 1 1 1 1 |   | b |   | P1 |
| 0 0 1 0 | x | c | = | R0 |
| 3 2 1 0 |   | d |   | R1 |
    H       x   C   =   G

H x C = G
H-1 * G = C

Inverse of H
|  2 -2  1  1 |   | P0 |   | a |
| -3  3 -2 -1 |   | P1 |   | b |
|  0  0  1  0 | x | R0 | = | c |
|  1  0  0  0 |   | R1 |   | d |
```

## Bezier Curves

* Defined by n+1 points (n = degree of equation)
* Line
    * Pt moves along line P0P1
    * P<sub>t</sub> = P<sub>0</sub>(1 - t) + tP<sub>0</sub>
* Quadratic
    * Given P<sub>0</sub>, P<sub>1</sub>, P<sub>2</sub>
    * Q<sub>0</sub> moves along the line P<sub>0</sub>P<sub>1</sub>
    * Q<sub>1</sub> moves along the line P<sub>1</sub>P<sub>2</sub>
    * Q<sub>t</sub> moves along Q<sub>0</sub>Q<sub>1</sub>, and is on the parabola
    * Qt = (1-t)Q0 + tQ1
    * (1-t)[(1-t)P<sub>0</sub> + tP<sub>1</sub>] + t[(1-t)P<sub>1</sub> + tP<sub>2</sub>]
    * (1-t)<sup>2</sup>P<sub>0</sub> + 2t(1-t)P<sub>1</sub> + t<sup>2</sup>P<sub>2</sub>
* Cubic
    * Given P<sub>0</sub>, P<sub>1</sub>, P<sub>2</sub>, P<sub>3</sub>
    * R<sub>t</sub> moves along the line R<sub>0</sub>R<sub>1</sub>
    * R<sub>0</sub> moves along the quadratic Q<sub>0</sub>Q<sub>1</sub>
    * R<sub>1</sub> moves along the quadratic Q<sub>1</sub>Q<sub>2</sub>
    * R<sub>t</sub> = (1-t)<sup>3</sup>P<sub>0</sub> + 3(1-t)<sup>2</sup>P<sub>1</sub> + 3t<sup>2</sup>(1-t)P<sub>2</sub> + t<sup>3</sup>P<sub>3</sub>
    * Multiplying out to get standard form: = at<sup>3</sup>+bt<sup>2</sup>+ct+d
        * a = -P<sub>0</sub> + 3P<sub>1</sub> - 3P<sub>2</sub> + P<sub>3</sub>
        * b = 3P<sub>0</sub> - 6P<sub>1</sub> + 3P<sub>2</sub>
        * c = -3P<sub>0</sub> + 3P<sub>1</sub>
        * d = P<sub>0</sub>

```
| -1  3 -3 1 |   | P0 |   | a |
|  3 -6  3 0 |   | P1 |   | b |
| -3  3  0 0 | x | P2 | = | c |
|  1  0  0 0 |   | P3 |   | d |
```
