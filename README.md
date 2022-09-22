# assignment-2

This is the second assignment of the semester for HES 505.

The second part of the course was designed to introduce basic operations with vector and raster data. These operations will form the basis for building the spatial databases that underlie the bulk of statistical analyses we'll conduct in this class and probably in your graduate research. This homework is designed to give you practice building your spatial workflow and using the various functions we've learned to maniputlate both vector and raster data. By the end of this assignment you should be able to:

* Use __predicates, measures, and transformations__ to clean, subset, and change vector data

* Alter the resolution, extent, and data values of rasters

* Build new datasets based on the relations between vector and raster data

## Instructions

1. After you've joined the assignment repository, you should have this file (named Readme.md) inside of a R project named assignment-1-xx where xx is your github username (or initials). All of the data should be accessible on the server at `/opt/data/2022/assignment02/`.

2. Once you've verified that you've correctly cloned the assignment repository, create a new Quarto document. Name this file assignment-2-xxx.qmd and give it a title (like M Williamson Assignment 2). Make sure that you select the html output option (Quarto can do a lot of cool things, but the html format is the least-likely to cause you additional headaches). We'll be using Quarto throughout the course so it's worth checking out the other tutorials in the getting started section.

3. Copy the questions below into your document and change the color of their text.

4. Save the changes and make your first commit!

5. Answer the questions making sure save and commit at least 4 more times (having 5 commits is part of the assignment).

6. Render the document to html (you should now have at least 3 files in the repository: Readme.md, assignment-1-xx.qmd, and assignment-1-xx.html). Commit these changes and push them to the repository on GitHub. You should see the files there when you go to github.com.


## Vector data

### Packages and datasets
The [`tigris`](https://github.com/walkerke/tigris) package provides a number of handy functions for accessing different US geographic regions based on the US Census and the TIGER (Topologically Integrated Geographic Encoding and Referencing) system. You can download states (using `states()`), counties (using `counties()`), etc and have all of the objects returned as `sf` objects. Check out the package webpage to get a sense for what it can do!

For the next few weeks, we'll be using data from the High Country News [Land Grab University](https://www.landgrabu.org/) project. These data depict the role of expropriated Indigenous land in funding the fifty-two land-grant universities in the United States. They contain information on nearly 11 million acres of Indigenous land taken from ~250 Tribes, bands and communities through a multitude of treaties and violent land seizures. Check it out as it will help you understand what these data are depicting.

One of the other datasets we'll use fairly regulrarly during this class is the United States Protected Areas Database ([PAD-US](https://www.usgs.gov/core-science-systems/science-analytics-and-synthesis/gap/science/protected-areas)). PAD-US is America’s official national inventory of U.S. terrestrial and marine protected areas that are dedicated to the preservation of biological diversity and to other natural, recreation and cultural uses, managed for these purposes through legal or other effective means. The PADUS provides a lot of interesting information on land tenure arrangements in the US. Ecologists often rely on comparisons to these protected ares to understand the effects of anthropogenic change. Finally, you'll probably have to make a map at some point in your life and these protected areas are often useful tools for helping 'orient' people to the landscape you are mapping. As an additional bonus, the geometries in this dataset can be a real challenge to work with so you'll get a chance to practice some important diagnostics and trouble-shooting. For this assignment, we have restricted the data to the "Designation" type (i.e., protected via means not requiring Congress) in the Western US.


### Practicing with vector data

The data for this lab are in our shared folder (located at `/opt/data/2022/assignment02/`). There are several shapefiles in that folder (denoted by the `.shp` suffix in the file name). 

1. Load the `landgrab_parcel.shp` dataset. What is the CRS? How about the extent? Lastly, are the geometries valid? If not, make them valid. Show your code.

2. Load the `PA_designation.shp` dataset. What is the CRS? How about the extent? Lastly, are the geometries valid? If not, make them valid. Show your code.

3.  Project all of the vector datasets to the same CRS. Show your code. How did you choose which CRS to use?

4.  Now buffer the entire `PA_designation.shp` features by 50km and calculate the resulting area. What is the area of the largest buffered PA? Show your code.

3. Subset the entire `landgrab_parcel.shp` so that it only contains parcels that overlap your boffered `PA_designation.shp` object. How many parcels overlap the buffered PAs? How big is the largest parcel? What state has the most parcels that overlap the buffered PAs?

4.  Use the `tigris::states()` function to download state boundaries and filter them so that you only have the boundary for the state that contains the most parcels (from step 3). Show your code.

5. Crop the `landgrab_parcel.shp` and `PA_designation.shp` objects using your state boundary. How many features remain after you've cropped the datasets? Show your code.


## Raster Data

We're going to evaluate the current conditions are of the parcels that were sold in and around protected areas using two different raster datasets. The first comes from the [PLACES lab](https://placeslab.org/places/) at Boston University. This data depict land values across the contiguous United States at a fairly high resolution. The PLACES data was developed to better understand the costs, benefits, and motivaitons for private land conservation. The development and validation of this data is described in this [article](https://www.pnas.org/content/117/47/29577). The second is a categorical raster from the National Land Cover Dataset downloaded via the [`FedData`](https://github.com/ropensci/FedData) package. `FedData` downloads the file as a `raster` so you'll need to convert it to a SpatRaster. Similarly, you need to give the `get_nlcd` function a `Spatial` object so you'll need to convert your cropped parcel dataset to a SpatialPolygonsDataframe (using `as(parcelname, "Spatial")`. See the helpfile for more info.

### Practicing with vector data

6. Load the `places_fmv_all.tif` file as a SpatRaster and download the 2019 NLCD for the state with the most parcels (from step 3) data (using `FedData::get_nlcd()`). What CRS are the SpatRasters in? What is their resolution?  How do the extents compare? Show your code.

7. The two rasters don't align. Write out the pseudocode for the steps hyou would take to get them into alignment.

8. Dealing with differing resolutions can be tricky and there are a few options for either upscaling fine resolution data or downscaling coarse resolution data. What are they and what are the benefits/drawbacks of each approach?

9. Based on your answers to number 7 and 8 process the rasters so that their CRS, resolution, and extents align. 

10. We might be concerned about mapping errors in the NLCD dataset (sometimes pixels get misclassified). Let's smooth that layer out by applying a 5x5 moving window. Make sure that you drop the NAs.
      

## Integrating the two

Now that you have a cropped parcel layer that depicts the parcels that are within 50km of protected areas and two rasters that have the same CRS, resolution, and extent; let's integrate them a bit. 

11. Generate a new SpatRaster depicting the distance from all pixels that are classified as "Evergreen Forest" in the NLCD layer. You'll need to reclassify the smoothed NLCD layer so that all values that aren't "Evergreen Forest" are set to NA and then use `terra::distance` to generate the estimate.

12. Stack the distance raster and the land value raster (you may have to align them a bit). Then extract the mean values for each variable within each of your parcels (from step 5). Remember, that you'll need to make sure the parcels have the same CRS as the stack.

13. Now extract the land cover from your smoothed raster. What is the dominant landcover type of the first 10 parcels in that dataset.  
