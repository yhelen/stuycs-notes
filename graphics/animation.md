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

## New Commands

### transformation

```
transformation args knob
```

If there is a knob, look up its value and modify args by it

### frames

```
frames #
```

Set internal # of frames variable

### basename

```
basename name
```

Set internal frame name variable

### vary

```
vary knob startframe endframe startval endval
```

Compute and store the knob values for each frame


## 3-Pass Animation Framework

1. Setup
    * Set frames if frames command is present
    * Set basename if basename command is present
    * Stop if vary is present but not frames
2. Vary
    * Compute and store all knob values for every frame
    * Stop if the vary range is invalid
3. Draw
    * Repeat the loop for each frame
    * Update knobs in symbol table at the start of each loop
    * At end of each loop, save the current frame
    * Make animation

## Storing Knob Values

* Knob Major, Frame Minor (List of Knobs, each a list of frames)
* Frame Major, Knob Minor (List of Frames, each a list of knobs) -- easier
* If there is a hole between frames (vary does not define knob values for
  frames 7 and 8, for example)
