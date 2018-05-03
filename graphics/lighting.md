# Lighting

Colors are modeled based on:
1. Color, intensity, and location of light
2. Reflective properties of objects

## Types of Light

* Ambient Light: general lighting of an image
    * a single source - comes from all locations equally
    * represented by a normal color value
* Point Light: comes from a specific location
    * can have many sources for an image
    * we will assume the light is from very far away
    * represented by a color and location

## Phong Reflection Model

Models real world reflections by breaking them into 3 parts.
I (color, normalization) = ambient + diffuse + specular

diffuse and specular are point light

I = A·K<sub>a</sub> + P·K<sub>d</sub>·(N · L) + PK<sub>s</sub>[(2(N · L)N - L) · V]<sup>x</sup>

### Ambient Light

* A - Ambient Light (0->255)
* K<sub>a</sub> - constant of ambient reflection(0->1)
* Ambient light = A·K<sub>a</sub>

### Diffuse Reflection
Reflection of a point light source. Reflected evenly in all directions. These are things that have a matte/dull finish.

Some important things
P - color of point light source
K<sub>d</sub> - constant of diffuse reflection

```
 L    N
  \   |
   \  |
    \θ|
_____\|______
```

We can model the strength of the reflection with cosθ.

cosθ = N · L
diffuse = P · K<sub>d</sub> · (N · L)

### Specular Reflection

Reflects a point light source in a specific direction (shiny/glossy surfaces).

```
 L    N    R
  \_R_|_S_/   idk how to diagram it, but there is also another 
   \  T  /    view vector V between N and the x-axis. 
    \θ|θ/     the angle between V and R is α
_____\|/______
```

* P - color of point light
* Ks - constant of specular reflection
* R = T + S
* S = T - L
* R = 2T - L
