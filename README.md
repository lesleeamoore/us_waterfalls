
# Cascading Water in the Lower 48  


## Project Contents

- [Data Source](#data-source)
- [Project Background](#project-background)
- [Purpose](#purpose)
- [Mapmaking Process](#mapmaking-process)
- [Link to Final Project](#final-project-link)

***

### Data Source

Information for waterfall locations in the conterminous U.S. were found on the [USGS website](https://www.sciencebase.gov/catalog/item/5e8d2b5982cee42d13466001).

Elevation data came from the USGS NED 1/3 arc-second raster digital elevation model found [here](https://apps.nationalmap.gov/downloader/). Search coordinates used to locate Taughannock Falls in New York were -76.610502, 42.535608.

Background information was gleaned from a 2013 article by Brian J. Hudson, PhD, [Waterfalls, science and aesthetics](https://doi.org/10.1080/08873631.2013.828482) that appeared in the Journal of Cultural Geography.

Background information on Taughannock Falls was found in [National Geographic Guide to State Parks of the United States](https://www.google.com/books/edition/National_Geographic_Guide_to_State_Parks/nF92MKfiuksC?hl=en&gbpv=1&pg=PA54&printsec=frontcover).


Initial Data projection: NAD83/EPSG:4269

Final Map projection:  NAD83/EPSG:4269

### Project Background

  Most people in the United States have heard of Niagara Falls, and most Kentuckians know Cumberland Falls.  I have long wondered how many other waterfalls there are in the U.S. and where they are located.  To my astonishment, USGS data from 2017 lists 11860 falls in the conterminous U.S. alone.  The World Waterfall Database tells us that if we were to include Alaska and Hawaii, the number jumps to more than 17000.

  According to geographer Brian J. Hudson, waterfalls were long neglected in scientific research.  It has only been in the past 40 years or so that scientists have begun to study them intensely, especially in the context of human impact on waterfalls. He writes, "Today, these landforms attract the attention of scientists and scholars from a wide range of disciplines. As features of the landscape under threat from a variety of human activities, waterfalls are especially worthy of our serious attention." 

### Purpose

The purpose of the project is to locate natural waterfalls in the continguous 48 states of the U.S. as a first step to understanding the particular role of each in culture and science as well as the current status of their health.  The focus of this map is on Taughannock Falls near Trumansburg, New York.  This plunge-type waterfall was selected because, at a height of 215 feet, it is taller than Niagara Falls and "is the tallest single-drop waterfall east of the Rocky Mountains", according to the Taughannock Falls State Park website.  

### Mapmaking Process

The first step in process of making this map was to download the [USGS waterfall database GeoJSON file](https://doi.org/doi:10.5066/P9QQTKA0).  From that list, I selected Taughannock Falls in New York as my focus.  

Next, I downloaded elevation data from USGS centered on the coordinates for the waterfall. 

Mapmaking could then commence, first by using QGIS 3.32 Lima to create the map layers, and then importing those layers into Mapbox to produce the final map.

***Steps followed in QGIS to produce the contour map layer:***

![Alt text](<QGIS_screenshots_for_readme/2. Adding USGS raster layer.jpeg>)**1. Add USGS raster to QGIS.**

 ![Alt text](<3. Uploading GeoJSON waterfalls file-1.jpeg>)![Alt text](<4. Selecting Taughannock Falls.jpeg>)**2. Add USGS waterfalls GeoJSON layer, and query the file for Taughannock Falls.**

![Alt text](<5. Site placed and scale fixed to 5000 feet.jpeg>)**3. With the site placed, fix scale at 5000 feet.**

![Alt text](<6. Settings for raster clip.jpeg>)![Alt text](<7. Clipped raster layer.png>)**4. Clip the raster by the extent of the layer.**

![Alt text](<8. Raster Calculator.png>)![Alt text](<9. Layer including raster calculations.jpeg>)***5. Using the raster calculator does the algebra for us, setting the stage for the extracting the contour lines.***

![Alt text](<10. Extracting Contours.png>)![Alt text](<11. Contours in place.png>)**6. Elevation contours with 20-foot intervals give a good visulization of elevation change while allowing for easy reading of the lines.**

![Alt text](<12. Using the field calculator to determine index lines.jpeg>)![Alt text](<13. Results of field calculation.png>)**7. With contours in place, we use the field calculator to determine our index lines.**

**8. Last, we need to compress the contours shapefile so that it can be uploaded to Mapbox.  If you are using a MacBook or iMac, you may need to first upload the files to something like Google Drive, then compress them from there.  Mapbox does not always recognize files zipped directly from the Mac.**



***Steps followed on Mapbox to produce the final map:***

**1. After creating my new account in Mapbox, my first step was to upload the USGS waterfalls data.  Becasue the file was so large, and at Mapbox's suggestion, I uploaded it directly as a tileset rather than a dataset.**

**2. Next, upload the contours shapefile that had been compressed using Google Drive.**

**3. After selecting "Styles" from the menu on the right, select "New Style" and choose a base, in this case Satellite Streets.**

**4. A search for Taughannock Falls, NY, brought the map close to the coordinates, which were then fine-tuned to center on the falls. Selecting "Settings" from the top menu bar, lock the coordinates so that the map will always open to this point.**

**5. Click on the + in the panel on the left to add a new custom, the contours tileset, to the map. Change the contour line color to one that will be easy for users to see. Select an opacity level of less than 1 so that the contours do not dominate the map, then choose "Style across zoom range" so that they fade out before the edge of uploaded contour layer is reached.**

**6. The area around the falls is steep, so it is helpful to add index lines.**

**7. To label those lines and make other changes to the map text, duplicate this layer by choosing the icon next to the plus sign in the panel on the left. Under "Select data", change the setting to "Symbol".**

**8. To add labels to the index contour lines, first select "Style" and "Text".  Select "Text field" -> "Add a data field" -> "ELEV". Change the color to white and the opacity to 0.8.  Then set the halo color to black and the width and blur to 2 px.**

**9. Select the "Placement", two tabs to the right of "Text", to position the labels on the lines."**

**10. Then go to "Select data" -> "Filter" and set the index filter to 1.**

**11. Add the waterfalls layer by selecting "Add layer" -> "Custom layer" and choosing the waterfalls_us tileset.  Then change the data type to "Symbol".**

**12. Now we're ready to add an icon to the waterfalls layer.  To upload the waterfalls icon, select "Images" from the top menu bar -> Upload images -> Select file.**
*Note: I downloaded a free waterfall icon from https://icons8.com/icons/set/waterfall as an .svg file, which I then edited in Visual Studio Code, changing the size parameter from percentage to pixel size so that the icon could be made smaller. To do that, I deleted with "width=100%" line.*

**13. In the waterfalls layer, select the icon under the "Icon" tab.**

**14. To identify the points on the map where the icon should appear, select "Text" -> "Text field" -> "Insert a data field" -> "name".**

**15. Change the text color to #c3b3f3 and the halo color to #02076f, with a halo width and blur of 1 px.**

**16. Under the "Position" tab, change the offset values to 0, 1.4., and anchor the text in the desired position relative to the icon.**

**17. Reorder layers, if necessary, by dragging/dropping them, then reset the map to its initial center and zoom level by unlocking and locking them in the "Settings" tab.** *Note: My settings are slightly different between the initial screenshot and this one because I did forget to lock them the first time, as I learned when I closed and reopened the style!*

**18. The last steps are to publish the map and get the necessary urls and tokens so the map will be accessible online. On the far right of the top toolbar, select "Publish" -> "Publish".  When the style is published, the urls and tokens can always be accessed by going to the Styles page and selecting the "Share your style" icon. A popup opens and contains the needed links.**



### Map summary

Mapmaking has moved into the digital age, and there are many tools and many ways available to create maps now.  Cartographers of yesteryear created hand-drawn maps that were also works of art.  Today, using free software and web-based programs such as QGIS and Mapbox, or paid programs such as ArcGIS, mapmakers create works that not only depict location but also tell a story or answer a question, whether those works are choropleth maps of wildfires or population densities or the impact of climate change on migratory bird paths.  This particular map can serve as a economic tool, helping tourists locate thousands of waterfalls across the lower 48 states of the U.S. or helping hydroelectric engineers locate possible new sources of renewable energy.  Or, it can, perhaps, satisfy the curiosity of the armchair traveler who just like to know where things are.


## Final Project Link

Please view the [final map online](https://lesleeamoore.github.io/us_waterfalls)

