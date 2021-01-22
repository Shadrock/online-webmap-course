# Metadata & Data Simplification
This file provides information for the `Zaatari_refugee_camp_water.geojson` and `Zaatari_refugee_camp_water_simplified.geojson` files in this folder.

The data in `Zaatari_refugee_camp_water.geojson` were downloaded from [OpenStreetMap](https://www.openstreetmap.org/#map=15/32.2931/36.3227&layers=H) using the [Overpass Turbo](https://overpass-turbo.eu/) query builder searching for nodes with the following query: `amenity=water_point OR amenity=drinking_water`. The data were collected on 29, October 2020. Information about the creation and structure of the data can be found on the [OSM wiki page for refugee camp mapping](https://wiki.openstreetmap.org/wiki/Refugee_Camp_Mapping).

## Data Simplification
The following steps were used to simplify the data and create the `Zaatari_refugee_camp_water_simplified.geojson` file.

1. Upload data to a converter (I used http://geojson.io) and save the data as a .csv file.
2. Open the .csv in the tabular editing program of your choice (I used Excel).
3. Remove `node/` from every record under the `@id` column using a find and replace.
4. Since I only want to show the water points and, perhaps, symbolize them by `type` I removed the following columns: `amenity`,	`district`,	`source`, and	`street`.
5. Simplify coordinates to the sixth decimal place. I did this by selecting all coordinates, formatting the cells as a number, and specifying the number of decimal places to be kept.
6. Re-convert the .csv to `GeoJSON` using an online converter: I used https://odileeds.github.io/CSV2GeoJSON/. I took the extra step of choosing to *not* keep the additional 'lat/lon' properties inserted by the converter since they would have been redundant.
