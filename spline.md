# Splines - Hermite Curves

Curves that can be combined smoothly.

for t: 0-1, t += step
* x = a<sub>x</sub>t<sup>3</sup>+b<sub>x</sub>t<sup>2</sup>+c<sub>x</sub>t+<sub>d</sub>
* y = a<sub>y</sub>t<sup>3</sup>+b<sub>y</sub>t<sup>2</sup>+c<sub>y</sub>t+<sub>d</sub>

Given Information:
* P0, P1: Endpoints
* R0, R1: Rates of change at endpoints
* f(t) = a<sub>x</sub>t<sup>3</sup>+b<sub>x</sub>t<sup>2</sup>+c<sub>x</sub>t+<sub>d</sub>: Points on curve
* f'(t) = 3a<sub>x</sub>t<sup>2</sup>+2b<sub>x</sub>t+c: Rates of change

When t=0 f(t) = d: P0
When t=0 f'(t) = c: R0
When t=1 f(t) = a + b + c + d: P1
When t=1 f'(t) = 3a + 2b + c: R1

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
