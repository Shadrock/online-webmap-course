# Learning GeoJSON
GeoJSON is an open standard format designed for representing spatial data and is the format we will be using for our web mapping studio assignments. GeoJSON is probably very different from most of the formats you have experience with already, such as `.shp` or raster files. GeoJSON is a plain-text format that is very common in web mapping. Because it is a type of "[JavaScript Object Notation](https://www.w3schools.com/whatis/whatis_json.asp)" it can easily be parsed with Javascript and is sometimes the best (or only) supported format by JavaScript web-mapping libraries including Leaflet, Carto, and Turf (which we will be using later in the semester).

Another advantage of GeoJSON is that it is fairly simple and can be read by humans. On the other hand, file-sizes may be quite large compared to other formats, but there are ways to reduce the file size, which we'll discuss briefly.

Let's take a quick look at a few common geometries using GeoJSON.

## Geometry in GeoJSON
Coordinates in GeoJSON are formatted in a simple decimal format. A position is an array of coordinates that should go in the following order: `[longitude, latitude, elevation]`. Geometries are shapes (e.g. points, lines, polygons). All simple geometries in GeoJSON consist of a type and a collection of coordinates.

_Points_ look like this:

```json
{
  "type": "Point",
  "coordinates": [-104.99404, 39.75621]
}
```
_Polylines_ are called `LineString` and they look like this:

```json
{
  "type": "LineString",
  "coordinates": [
      [-100, 40], [-105, 45], [-110, 55]
  ]
}
```
To represent a line, you’ll need at least two points to connect.

_Polygons_ look like this:

```json

{
  "type": "Polygon",
  "coordinates": [
      [[-104.05, 48.99], [-97.22,  48.98], [-96.58,  45.94], [-104.03, 45.94], [-104.05, 48.99]]
  ]
}
```
The list of coordinates for Polygons is nested one more level than that for LineStrings.

## Features

A 'Feature' is a combination of geometry is with non-spatial attributes, which are encompassed in a property named `properties`. These contain one or more name-value pairs  for each attribute. For example, the following "Feature" represents a geometry with two attributes, named "type" and "population":
```json
{
  "type": "Feature",
  "geometry": {...},
  "properties": {
    "type": "refugee camp",
    "population": 327238
  }
}
```
This geometry, then, likely represents a refugee camp and gives the camp population held by the geometry.

## GeoJSON Tools  
There are a host of different tools you can use to work with GeoJSON. When you're getting started, you'll likely want to know where to go to create, check, or convert GeoJSON files.

You can [create GeoJSON via this web interface](http://geojson.io) (which is also really good for checking to make sure a GeoJSON file you have is rendering properly); you can [convert `.shp` files to GeoJSON with ArcPro using these instructions](https://pro.arcgis.com/en/pro-app/tool-reference/conversion/features-to-json.htm); you can convert `.shp` files to .`kml` or `kmz` files (commonly used by Google Earth) and [convert them using Ogre](http://ogre.adc4gis.com), which also converts `.gpx` or `.csv` files; you could zip a `.shp` file and convert the zipped file to GeoJSON using [https://mapshaper.org/](https://mapshaper.org/) or [http://gipong.github.io/shp2geojson.js/](http://gipong.github.io/shp2geojson.js/); and if that's not enough you can check out [this huge list of GeoJSON utilities](https://github.com/tmcw/awesome-geojson) to see what else is available.

As noted earlier, GeoJSON files can sometimes get quite large. There are a few tricks to keeping things lightweight:
- Removing attributes: often GeoJSON data (and data in general) contain columns or attributes that are unused and removing them reduces the file size.
- Quantization means reducing the precision of coordinates in your data to a certain level that isn’t noticeable on the map. In decimal degrees, coordinates to the sixth decimal place (`36.339179`) indicate a precision of around 5 inches. Unless you're trying trying to be incredibly precise for applications like engineering or property rights, this degree of precision will likely be more than enough. Often, I'll see coordinates in GeoJSON that are computer generated, contain way more than six decimal places, and don't really add any value in precision while adding a lot to the file size!
- Simplification will eliminate details that aren’t visible at reasonable zooms - removing coordinates from LineStrings and Polygons that are super close together is another way to reduce file size ([see an example here](https://mourner.github.io/simplify-js/)).

We'll specifically walk through both removing attributes and quantization in Studio 5.

# Further Reading
This is a brief overview to get you started and more detailed information such as creating GeoJSON maps in Github and simplifying GeoJSON is provided in the appropriate studios. However, if you want to dive more deeply into the world of GeoJSON, here are a few great resources:
- Leaflet has [a nice short blog post about GeoJSON](https://leafletjs.com/examples/geojson/).
- The geographer/cartographer/developer Tom MacWright has a great, [slightly more detailed blog post about GeoJSON here](https://macwright.org/2015/03/23/geojson-second-bite.html).
- The University of Ben-Gurion in Israel also provides [an in-depth, discussion of GeoJSON](http://132.72.155.230:3838/js/geojson-1.html) and, of course,
- you can always visit [the official documentation](https://geojson.org/)!
