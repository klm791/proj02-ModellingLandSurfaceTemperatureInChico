# Project 02 Proposal: Modelling Land Surface Temperature Across Chico

**Team members:** Kristian Meza

See the [Project 02 instructions](https://data385.github.io/project/proj02_wholegame.html) for what goes in each section. Bullet points are great. Put any images in an `img/` folder.

## 1. Problem statement

Considering how hot Chico can get in the Summer, urban planners may be concerned with identifying which physical landscape characteristics are most strongly associated with higher land surface temperature (LST) within the city. Understanding these relationships allows for improved identification of areas that may warrant heat mitigation planning to improve environmental conditions and minimize excess surface heat. I would expect that the Normalized Difference Vegetation Index (NDVI) would have a negative relationship with LST, while the Normalized Difference Built-up Index (NDBI) would show a positive association. Elevation may have a weak negative relationship with LST.

## 2. Research question

How strongly are NDVI, NDBI, and elevation associated with land surface temperatures in Chico?

## 3. Data acquisition

### a. Confirm viability

I intend to collect a raster file containing California’s land cover classifications from the Multi-Resolution Land Characteristics Consortium (NLCD); Landsat spectral/thermal satellite scenes, and a digital elevation model (DEM) will both be sourced from the United States Geological Survey. I will also acquire a shapefile for Chico's city limits from the California State Geoportal. All of the data is sourced from official government agencies intended for public use.

The thermal and spectral data are collected by Landsat sattelites while the DEM is produced from airborne lidar. The shapefile is just a digitized vector of the city limits created by the California Department of Technology. Landsat imagery is also used in order to classify the different types of land cover in the NLCD raster.

<https://earthexplorer.usgs.gov/>

<https://www.mrlc.gov/data>

<https://www.usgs.gov/3d-elevation-program>

<https://gis.data.ca.gov/datasets/california-city-boundaries-and-identifiers/explore?location=39.766878%2C-121.803342%2C13>

### b. Variables of interest

- LST - Quantitative, continuous, response. Surface temperature measurements in Celsius, derived from Landsat thermal infrared bands.

- NDVI - Quantitative, Continuous, predictor. An index derived from Landsat red and near-infrared spectral bands. It's used as an indicator of healthy vegetation.

- NDBI - Quantitative, continuous, predictor. An index derived from Landsat near-infrared and shortwave infrared bands. It's used as an indicator for identifying built up areas.

- Elevation - Quantitative, continuous, predictor. Elevation in meters derived from the DEM.

- Slope - Quantitative, continuous, EDA. Steepness of the terrain derived from the DEM

  - I'll likely figure out a more compelling variable at some point. If I end up having time it might be worth overlaying the predicted temperature model output over population density and map it.

- Land Cover - Categorical, nominal, EDA. The land cover category assigned to each raster cell sourced by the NLCD.

## 4. Data example

[PDF](data_management.pdf)

## 5. EDA

I anticipate I’ll use the terra package to import and prepare the rasters before I finish wrangling the data using the tidyverse functions. Terra’s rast() function will import the Landsat bands, the DEM, and the NLCD land cover file. I’ll then remove the observations that fall outside of the Chico city extent shapefile using terra’s crop() and mask() functions. Once the layers are aligned and clipped, I’ll combine them all into a single dataframe where each row represents an individual cell in the raster. I could also use glimpse to make sure that the data is organized correctly once that’s done.I will use select() to keep the variables needed for analysis and filter() to remove any unusable observations. Through mutate(), I’ll scale and convert the raw raster data into interpretable values. The function summarise() will be useful for attaining descriptive statistics for the quantitative variables, and if paired with group_by(), I can compare the LST across the different land cover types. I can create histograms of the quantitative variables using ggplot so I can then visualize their distributions. I’ll use scatter plots to see how each of my predictor variables is associated with LST. A boxplot would also be a nice addition to see how LST relates to the land cover classes.

## 6. Modeling

I’ll use a multiple linear regression model to see how physical landscape characteristics are associated with land surface temperature across Chico. LST will be the response variable, while I’ll use NDVI, NDBI, and elevation as the predictors. A multiple linear regression fits my research question because I intend to estimate how strongly each predictor is associated with LST while accounting for the other variables as well.

## 7. Communicate

I'll make a slideshow presentation that will include a variety of plots, maps, and summary statistics.

## 8. LLM disclaimer

I'll likely use Chatgpt to help with debugging my code. Fortunately, my data does not contain any sensitive. Regardless, I don't intend to upload my data to the LLM at all, as there's honestly just no need; more often than not, a screenshot of an error will help solve the problem.
