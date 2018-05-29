# Shading Models

How/when you calculate the color (I) for each shape

* Flat shading
    * Calculate I once per polygon
* Gouraud Shading
    * Calculate I for each vertex.
    * Interpolate I in scanline conversion and in draw line.
* Phong Shading Model
    * Calculate I once per pixel
    * Interpolate the vertex normal in scanline conversion and draw line.

Calculating Normals for Gouraud and Phong Shading
* Vertex normals are the combined value of all surface normals for polygons
  that share a common vertex.
