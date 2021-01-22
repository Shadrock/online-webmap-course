# What's the deal with OSM data?
OpenStreetMap is a somewhat misleading name since it's more than a map, it's a huge crowdsourced database! What you see on the [OpenStreetMap homepage](https://www.openstreetmap.org/) - or other OSM tilesets for that matter - is a _selection_ of data available in the OSM database. For example, some people focus on features in the database related to [cycling](https://www.thunderforest.com/maps/opencyclemap/), while others focus on [humanitarian features](http://map.hotosm.org/#15/32.2916/36.3341). You can see [a list of OSM tiles here](https://wiki.openstreetmap.org/wiki/Tiles) and view a few of the different tiles on the OSM homepage under the *Layers* icon on the right side of the screen. To see the underlying data of a particular area (including data that aren't shown on the map), you can check the "Map Data" box. Be careful, though: depending on the area you are looking at, you may load tens of thousands of data points and crash your browser!

The example below shows how to view the Humanitarian OSM layer and see underlying data of Zaatari refugee camp in Jordan.

![Data view in OSM](images/OSM_data.png)

## The Structure of OSM data
OSM data are made of "elements" that are based on a "node" (analogous to points for GIS folks). Nodes can be separate or can be connected to create:
- _Ways_: a connected line of nodes (analogous to polylines). Used to create roads, paths, rivers, and so on.
- _Closed Ways_: ways that form a closed loop (usually created to form areas).
- _Areas_: closed ways which are also filled (analogous to polygons).
- _Relations_ that can be used to create more complex shapes, or to represent elements that are related but not physically connected.

For more details on these elements see this [OSM wiki page](https://wiki.openstreetmap.org/wiki/Elements).

All these elements can carry **tags**, which is a key=value pair describing what the element is. For instance, mapping a mobile phone store can be done by creating a node, and adding the following tags: `shop=mobile_phone`, `name=John Smith's phone centre`. For more details on tags see this [OSM Beginners Guide](https://wiki.openstreetmap.org/wiki/Beginners_Guide_1.3).

## Getting Data with Overpass Turbo
Now that we understand nodes and tags, we can find out what sort of data we want to get! There are a variety of ways to get at OSM data, but we'll be using [Overpass Turbo](http://overpass-turbo.eu/), which is an interactive query generator. The basics process for using Overpass Turbo is:

1. Zoom to the appropriate region on the map.
2. Enter your query in the left side of the page and trigger any actions using the buttons at the top. Your query will search OSM tags for the elements you want. If you are new to the query language use the wizard (we'll do this below).
3. Preview your data
4. Export your data!

The OSM wiki contains a [full description of the syntax of the query language](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL) and a [collection of examples](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_API_by_Example). Additionally, Mapbox has a nice page that walks through [using Overpass Turbo to get specific features from a ski resort](https://docs.mapbox.com/help/tutorials/overpass-turbo/).

## Data for Zaatari Refugee Camp
Now that we understand the role of tags for OSM data, we'll need to find the proper tags for the features we want. In general, you can do this by opening OSM and clicking a feature to find its tags, or by searching the [OSM Map Features wiki](https://wiki.openstreetmap.org/wiki/Map_Features) to find the keys and values that most closely resemble the features you want to query.

There are a significant number of humanitarian organizations that contribute to OSM through various projects. Well documented projects will have associated Wiki pages, such as [Missing Maps](https://wiki.openstreetmap.org/wiki/Missing_Maps_Project): a collaboration between the Humanitarian OSM Team (or "HOT"), and partners such as The American Red Cross, British Red Cross, and Médecins Sans Frontières. Another example is refugee camp mapping done by [REACH](https://www.reach-initiative.org/what-we-do/), which is an organization often supported by the United Nations to conduct field surveys or map refugee camps.

Searching OSM wiki for "REACH camp mapping" takes us to [the page for refugee camp mapping](https://wiki.openstreetmap.org/wiki/Refugee_Camp_Mapping#Common_Tags_for_Site), which includes tags, and a case study of Zaatari refugee camp: perfect! The tags used for refugee camp mapping provide a wide range of information important for humanitarian programs. Let's take a closer look at the [elements relating to water](https://wiki.openstreetmap.org/wiki/Refugee_Camp_Mapping#Drinking_Water).

Water distribution in refugee camps is critical and mandated by the [SPHERE standards](https://spherestandards.org/), which sets standards for humanitarian action to promote quality and accountability. The SPHERE handbook sets forth standards such as how much water the resident of a camp should have access to and a maximum distance that one should have to travel to access water: less than 500 meters ([see the handbook chapter on water here](https://handbook.spherestandards.org/en/sphere/#ch006_004)).

A practical GIS analysis of water accessibility in a refugee camp, then, is ensuring that all portions of the camp are within 500 meters of a water distribution point of some sort. To do this, we need to find those nodes! There are several different tags for water in OSM, but we'll focus on `amenity=water_point` and `amenity=drinking_water`.

**Let's get some data:**

1. Start by using the search tool in Overpass to locate `zaatari, jordan`. The search tool is located on the map to the right of the zoom buttons.
2. Once you've located and zoomed to Zaatari, zoom in to see some of the features, then zoom out until the whole camp is within the Overpass map view.
3. Click the **Wizard** button from the toolbar and paste the following statement in the Query Wizard window: `amenity=water_point OR amenity=drinking_water` since these are the keys and values we found in the camp mapping wiki.
4. Click **Run** and Overpass will highlight the features on the map. You can click on individual nodes to see more information about them (see example below).

![Data view in OSM](images/Overpass_query_mapview.png)

Additionally, you can select the **Data** tab (next to the **Map** tab in the upper right hand side of the map view) to more closely inspect the data (see example below)
![Data view in OSM](images/Overpass_query_dataview.png)

5. Once everything looks good, export them by clicking the **Export** button in the toolbar, and select GeoJSON.

Although we've previewed our data, you can also check your downloaded data by viewing it in https://geojson.io or using [Github to automatically render a GeoJSON file in a repo as a map](https://docs.github.com/en/free-pro-team@latest/github/managing-files-in-a-repository/mapping-geojson-files-on-github).

Congratulations, you've got some data! Now let's make it more performant for our needs.

# The Importance of Data Simplification
GeoJSON is a great data format, however, it can be unnecessarily large. Removing any properties that are not necessary for your visualization and using a maximum of 6-decimal places for the precision for coordinate values can help radically reduce the size of your dataset, which in turn can improve web map performance. The degree to which you simplify your data depends entirely on what you plan to do with it, but very often GeoJSON datasets will contain far more information than is needed and considering what you really need is important. This [GIS Stack Exchange post](https://gis.stackexchange.com/questions/8650/measuring-accuracy-of-latitude-and-longitude/8674#8674) does a nice job of providing more detail.

There a variety of tools that can be used to simplify GeoJSON and [this Mapbox post is a good resource](https://docs.mapbox.com/help/troubleshooting/working-with-large-geojson-data/) for further ideas about simplification and links to current tools. My methods are listed below in detail. For our purposes, we only need to keep on of the properties of the data and we really only need precision within 1 meter.

## Simplify Your OSM Data
When I originally downloaded the data for this tutorial, the file size was `397kb`. This is a relatively small dataset, but by following the steps listed below, it was further reduced to `134kb`: a reduction by almost 67 percent! You can imagine what a difference this might make with a truly large dataset. As shown in the snippet below, there are several properties in the data that we will not use and the precision of the coordinates are unnecessarily extended to seven decimal places, which is suggesting precision in centimeters.

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

The following steps were used to simplify the data and create the `Zaatari_refugee_camp_water_simplified.geojson` file found in the data folder.

1. Upload data to a converter (I used http://geojson.io) and save the data as a .csv file.
2. Open the .csv in the tabular editing program of your choice (I used Excel).
3. Remove `node/` from every record under the `@id` column using a find and replace.
4. Since I only want to show the water points and symbolize them by `type` I removed the following columns: `amenity`,	`district`,	`source`, and	`street`.
5. Simplify coordinates to the sixth decimal place. I did this by selecting all coordinates, formatting the cells as a number, and specifying the number of decimal places to be kept.
6. Re-convert the .csv to `GeoJSON` using an online converter: I used https://odileeds.github.io/CSV2GeoJSON/. I took the extra step of choosing to *not* keep the additional 'lat/lon' properties inserted by the converter since they would have been redundant.

Congratulations: you now have a **simplified** and *better performing*, dataset! Happy mapping!

# Citations & Further Info
This tutorial pulled text from a variety of sources including the [Mapbox tutorial on incorporating OSM data](https://docs.mapbox.com/help/tutorials/overpass-turbo/), the [LearnOSM web page for OSM data](https://learnosm.org/en/osm-data/), and the [OSM Beginners Guide](https://wiki.openstreetmap.org/wiki/Beginners_Guide_1.3).
