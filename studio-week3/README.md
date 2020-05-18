# Welcome to the Studio Week 3!
So far, we've learned how to set up web pages and embed some pre-existing maps, and then create new base maps with basic markers. This week we'll be working on creating choropleth maps and adding more interactivity.  

**A brief reminder:** some of these tasks require you to look for comment code in the files to guide you. As a refresher, `<! -- Comments in HTML that look like this -->` and comments in Javascript `// use two slashes like this.`

## Expected Outputs for this week / what to submit: 
As with last week, you will submit a link to your Github repo and the working website that it hosts. While we have included starter `.html` files for you, they are quite basic: you're going to need to use the tutorials below, in conjunction with your previous files and everything you've learned up to this point to build your website, debug it, etc.

1. `index.html` - Start with [this Mapbox tutorial for creating a style for a choropleth map](https://docs.mapbox.com/help/tutorials/choropleth-studio-gl-pt-1/). This tutorial will include downloading sample data, then uploading them *to your Mapbox account.* Once you've completed that, move on to [this tutorial that will show you how to add interactivity to your map](https://docs.mapbox.com/help/tutorials/choropleth-studio-gl-pt-2/). In your final map, make the following edits to the CSS style in your header: Update `#map` and `#features` from`top: 0;` to `top: 200px;`
2. `mapbox-interaction.html` - Next, we'll explore adding some functionality in Mapbox. Open the file and look for the comment code that prompts you to add certain types of interactivity and gives you a place to start looking for documentation. This is a very common challenge when creating a webmap: you want to do something, but you're not sure how! So you have to look around at documentation and other people's code to find the answer. As you go through this exercise remember how much emphasis we put on good documentation in my classes...  
3. `mapbox-turfjs.html` - Finally, we're going to introduce some analytical capability to our maps. [Follow this Mapbox tutorial for creating a map that can do some basic analysis on point data](https://docs.mapbox.com/help/tutorials/analysis-with-turf/). Note that the **Getting started** and **Add Structure** sections of the tutorial have already been completed in the `mapbox-turfjs.html` starter file. 

<!--- This exercise was commented out because the tutorial is missing some lines of code. For example, in the attribution, they leave '...' as the parameter. They don't specifically mention that this should be replaced and throws an error if it isn't. 2. `starter-file-2-name-here` - After completing the first exercise in Mapbox, we're going to build a similar map in Leaflet. This is good for getting familiar with different Javascript libraries and getting used to syntax differences between Leaflet and Mapbox (you can also list both Leaflet and Mapbox on your resume!). [Use this Leaflet tutorial to create the interactive choropleth map](https://leafletjs.com/examples/choropleth/). --->

**At the end of the week you will submit a link to your repo via Moodle.** Happy coding!

## For those who want to explore the basics more: 
- If you want to explore Leaflet more, you can follows this [Leaflet tutorial for adding basic geographic features (point, polygon, polyline) to a map](https://github.com/jakobzhao/geog371/tree/master/lectures/lec07). You will need to set up a new `.html` file from scratch.  
- Alternatively, the [Leaflet website hosts a variety of tutorials](https://leafletjs.com/examples.html). Most of these tutorials assume that you can set up a basic html file, including body, header, and script tags. 

## For those who need a bigger challenge: 
After successfully following the instructions above you can take things further... these tutorials are more complex but allow for some really cool interactivity. They both require you to construct complete web pages. 
- Mapbox has a good tutorial for how to [build a Store Locator](https://docs.mapbox.com/help/tutorials/building-a-store-locator/) that includes some really cool interactivity.
- Here's a great Mapbox tutorial for how to [show changes over time](https://docs.mapbox.com/help/tutorials/show-changes-over-time/): this tutorial includes a 4MB GeoJSON file that contains 15,273 geocoded motor vehicle collision incidents in NYC. Github pages limits are 1GB, you should be able to host these data and the code in a repo! 
