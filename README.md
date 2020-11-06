# cobble
Render vector tiles to raster images with [Mapnik](https://github.com/mapnik/mapnik).

Cobble serves raster tiles through an embedded HTTP server; with a given set of vector tiles: 

    cbbl serve dataset.mbtiles

## Key features

* Meta-tiles: tiles are rendered in batches; by default one vector tile is rendered as 4x4 raster tiles. This is necessary for label placement across tiles.
* Pixel density: tiles can rendered at 72 dpi, @2x and @3x resolutions.

## Alternatives
* [mod_tile](https://github.com/openstreetmap/mod_tile)
* [tirex](https://github.com/openstreetmap/tirex)
* [TileStache](http://tilestache.org)

## Other Stuff
* [The smallest 256x256 single-color PNG file](https://www.mjt.me.uk/posts/smallest-png/)
