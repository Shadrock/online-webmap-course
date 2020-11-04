# Metadata & Data Simplification
This file provides information for the `Zaatari_refugee_camp_water.geojson` and `Zaatari_refugee_camp_water_simplified.geojson` files in this folder.

## The Importance of Data Simplification
GeoJSON is a great data format, however, it can be unnecessarily large. Removing any properties that are not necessary for your visualization and using a maximum of 6-decimal places for the precision for coordinate values can help radically reduce the size of your dataset, which in turn can improve web map performance. The degree to which you simplify your data depends entirely on what you plan to do with it, but very often GeoJSON datasets will contain far more information than is needed and considering what you really need is important. This [GIS Stack Exchange post](https://gis.stackexchange.com/questions/8650/measuring-accuracy-of-latitude-and-longitude/8674#8674) does a nice job of providing more detail.

There a variety of tools that can be used to simplify GeoJSON and [this Mapbox post is a good resource](https://docs.mapbox.com/help/troubleshooting/working-with-large-geojson-data/) for further ideas about simplification and links to current tools. My methods are listed below in detail.


# OSM Data
The data in `Zaatari_refugee_camp_water.geojson` were downloaded from [OpenStreetMap](https://www.openstreetmap.org/#map=15/32.2931/36.3227&layers=H) using the [Overpass Turbo](https://overpass-turbo.eu/) query builder searching for nodes with the following query: `amenity=water_point OR amenity=drinking_water`. The data were collected on 29, October 2020. Information about the creation and structure of the data can be found on the [OSM wiki page for refugee camp mapping](https://wiki.openstreetmap.org/wiki/Refugee_Camp_Mapping).

## Data Simplification
The data downloaded from OSM was originally `397kb`. This is a relatively small dataset, but by following the steps listed below, it was further reduced to `134kb`: a reduction by almost 67 percent! You can imagine what a difference this might make with a truly large dataset. As shown in the snippet below, there are several properties in the data that are not being used and the precision of the coordinates are unnecessarily extended to seven decimal places, which is suggesting precision in centimeters.

```GeoJSON
{
  "type": "Feature",
  "properties": {
    "@id": "node/3156233057",
    "amenity": "water_point",
    "district": "D8",
    "source": "REACH",
    "street": "street_11",
    "type": "Free_standing"
  },
  "geometry": {
    "type": "Point",
    "coordinates": [
      36.3391788,
      32.2811735
    ]
  },
```
By reducing the coordinate values by 1 decimal place we really don't loose any meaningful precision: the 6th decimal place equates roughly to precision of less than five inches! After following the steps below these data become:

```GeoJSON
{
      "type": "Feature",
      "properties": {
        "@id": 3156233057,
        "type": "Free_standing"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          36.339179,
          32.281174
        ]
      }
    },
```
Notice that several properties have been deleted and that coordinates have been shortened to the sixth decimal place.

The following steps were used to simply the data and create the `Zaatari_refugee_camp_water_simplified.geojson` file.

1. Upload data to a converter (I used http://geojson.io) and save the data as a .csv file.
2. Open the .csv in the tabular editing program of your choice (I used Excel)
3. Remove `node/` from every record under the `@id` column using a find and replace.
4. Since I only want to show the water points and, perhaps, symbolize them by `type` I removed the following columns: `amenity`,	`district`,	`source`, and	`street`.
5. Simplify coordinates to the sixth decimal place. I did this by selecting all coordinates, formatting the cells as a number, and specifying the number of decimal places to be kept.
6. Re-convert the .csv to `GeoJSON` using an online converter: I used https://odileeds.github.io/CSV2GeoJSON/. I took the extra step of choosing to *not* keep the additional 'lat/lon' properties inserted by the converter since they would have been redundant.

Congratulations: you now have a simplified, and better performing, dataset!
