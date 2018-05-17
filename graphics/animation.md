# Animation

Generate multiple images in a sequence with small changes between each.

Apply transformations over time.

```
move 400 0 0 0
     400 0 0 .25
     400 0 0 .5
     400 0 0 .75
     400 0 0 1

move 400 0 0 m0
```

`m0` is a knob

`vary` defines knob behavior

```
vary knob startframe endframe startval endval
```

e.g.
```
vary m0 0 4 0 1
```

This performs the transformations at the beginning.

`frames` defines the nmber of frames in an animation.

```
frames num
```

e.g. (5 frames above)
```
frames 5
```
