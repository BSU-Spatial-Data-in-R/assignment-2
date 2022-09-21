# assignment-2

This is the second assignment of the semester for HES 505.

The second part of the course was designed to introduce basic operations with vector and raster data. These operations will form the basis for building the spatial databases that underlie the bulk of statistical analyses we'll conduct in this class and probably in your graduate research. This homework is designed to give you practice building your spatial workflow and using the various functions we've learned to maniputlate both vector and raster data. By the end of this assignment you should be able to:

* Use __predicates, measures, and transformations__ to clean, subset, and change vector data

* Alter the resolution, extent, and data values of rasters

* Build new datasets based on the relations between vector and raster data

## Instructions

1. After you've joined the assignment repository, you should have this file (named Readme.md) inside of a R project named assignment-1-xx where xx is your github username (or initials). All of the data should be accessible on the server at `/opt/data/2022/assignment02/`.

2. Once you've verified that you've correctly cloned the assignment repository, create a new Quarto document. Name this file assignment-1-xxx.qmd and give it a title (like M Williamson Assignment 1). Make sure that you select the html output option (Quarto can do a lot of cool things, but the html format is the least-likely to cause you additional headaches). We'll be using Quarto throughout the course so it's worth checking out the other tutorials in the getting started section.

3. Copy the questions below into your document and change the color of their text.

4. Save the changes and make your first commit!

5. Answer the questions making sure save and commit at least 4 more times (having 5 commits is part of the assignment).

6. Render the document to html (you should now have at least 3 files in the repository: Readme.md, assignment-1-xx.qmd, and assignment-1-xx.html). Commit these changes and push them to the repository on GitHub. You should see the files there when you go to github.com.


## Vector data

### Packages and datasets
The [`tigris`](https://github.com/walkerke/tigris) package provides a number of handy functions for accessing different US geographic regions based on the US Census and the TIGER (Topologically Integrated Geographic Encoding and Referencing) system. You can download states (using `states()`), counties (using `counties()`), etc and have all of the objects returned as `sf` objects. Check out the package webpage to get a sense for what it can do!

For the next few weeks, we'll be using data from the High Country News [Land Grab University](https://www.landgrabu.org/) project. These data depict the role of expropriated Indigenous land in funding the fifty-two land-grant universities in the United States. They contain information on nearly 11 million acres of Indigenous land taken from ~250 Tribes, bands and communities through a multitude of treaties and violent land seizures. Check it out as it will help you understand what these data are depicting.

One of the other datasets we'll use fairly regulrarly during this class is the United States Protected Areas Database ([PAD-US](https://www.usgs.gov/core-science-systems/science-analytics-and-synthesis/gap/science/protected-areas)). PAD-US is America’s official national inventory of U.S. terrestrial and marine protected areas that are dedicated to the preservation of biological diversity and to other natural, recreation and cultural uses, managed for these purposes through legal or other effective means. The PADUS provides a lot of interesting information on land tenure arrangements in the US. Ecologists often rely on comparisons to these protected ares to understand the effects of anthropogenic change. Finally, you'll probably have to make a map at some point in your life and these protected areas are often useful tools for helping 'orient' people to the landscape you are mapping. As an additional bonus, the geometries in this dataset can be a real challenge to work with so you'll get a chance to practice some important diagnostics and trouble-shooting. For this assignment, we have restricted the data to the "Designation" type (i.e., protected via means not requiring Congress) in the Western US.




### Load vector data

The data for this lab are in our shared folder (located at `/opt/data/2022/assignment02/`). There are several shapefiles in that folder (denoted by the `.shp` suffix in the file name). 

1. Load the `landgrab_parcel.shp` dataset. What is the CRS? How about the extent? Lastly, are the geometries valid? If not, make them valid. Show your code.

2. Load the `PA_designation.shp` dataset. What is the CRS? How about the extent? Lastly, are the geometries valid? If not, make them valid. Show your code.

3. Use the `tigris::states()` function to download state boundaries and filter them so that you only have boundaries for WA, OR, ID, and MT. Show your code.

4. Project all of the vector datasets to the same CRS. Show your code. How did you choose which CRS to use?

## Raster Data

Speaking of land tenure, the raster dataset we'll use this week comes from the [PLACES lab](https://placeslab.org/places/) at Boston University. This data depict land values across the contiguous United States at a fairly high resolution. The PLACES data was developed to better understand the costs, benefits, and motivaitons for private land conservation. The development and validation of this data is described in this [article](https://www.pnas.org/content/117/47/29577).



