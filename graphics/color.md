# 01/31 Aim: Peering into the depths of color

## Color Depth

The amount of data used to present a single pixel.

| size   | color options                           |
| ----   | --------------------------------------- |
| 1 bit  | 1 color,  on / off                      |
| 2 bit  | 1 color, on / off, 1 bit for intensity  |
| 3 bit  | RGB, on / off                           |
| 4 bit  | RGB, on / off, 1 bit for intensity      |
| 6 bit  | RGB, each color has its own intensity   |
| 3 byte | RGB, each with 256 possible intensities |

### Other Color Spaces

#### RGBA

Red, Green, Blue + Alpha (transparency/opacity)

#### HSB

Hue, Saturation, Brightness

## Image File Formats

### Raster vs. Vector

Vector formats represent images as a series of drawing instructions.
Infinitely scalable. SVG (Scalable Vector Graphics)

Raster formats represent images as a grid of pixels.

### Uncompressed vs Compressed (Raster)

Uncompressed formats contain data for each pixel. (BMP, TIFF, RAW)

Compressed formats use a compression algorithm to minimize file size.

#### Lossless vs. Lossy

Lossless compression algorithms contain enough information to exactly
recreate the original image.
(PNG - Portal Network Graphics, GIF - Graphics Interchange Format)

Lossy compression algorithms do not retain all the details of the original
image.
(JPEG - Joint Photograhic Experts Group)

### PPM (Portable PixMap)

Uncompressed raster format.
Pixel data is presented by RGB triplets i either ASCII or binary.
All whitespace is equivalent.

Example File:
```
P3
4 3
255
255 0 0     255 0 0     255 0 0     255 0 0
0 255 0     0 255 0     0 255 0     0 255 0
0 0 255     0 0 255     0 0 255     0 0 255
```
