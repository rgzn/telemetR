# Collar Data Export
*0.80.1*

A Shiny application to extract GPS collar data from NDOW's GPS collar data warehouse.

## Justification

We have organized all GPS collar location data ( >1.8 million records) into a single database yet all data output is limited to SQL statements and Microsoft Excel line limit (65,000 rows). This application provides a user interface for interactively and visually selecting GPS location data for export.

The application also provides an GUI for exploratory data analysis and visualization. Users can estimate basic home range and utilization distributions, and plots of standard movement parameters.

## Use Case

The application can be used anytime a subset of GPS collar data is needed for analysis. The collar manufacturer's website will be the most up to date data, if required use their proprietary applications.

### Brownian Bridge Movement Models

The location data for one Rocky Mountain bighorn sheep was exported to analyze the expected movement path using Brownian bridge movement models.

![bbmm export](https://e3a0a746a3d3c5fa95928f1d69a3e9079c622a5f.googledrive.com/host/0B1OupsoLNZvkYTdtVFRIelBoN00/bbmm_example.jpg)

### Quantifying Migration

The location data for on mule deer was exported to quantify migration by plotting the net squared displacement against time.

![bbmm export](https://e3a0a746a3d3c5fa95928f1d69a3e9079c622a5f.googledrive.com/host/0B1OupsoLNZvkYTdtVFRIelBoN00/nsd_example.jpg)

*check the Migration Tab for more information.*

## Requirements

Download and install the latest versions of R [(R version 3.2.x)](https://cran.r-project.org/bin/windows/base/) and RStudio [(RStudio Desktop 0.99.x)](https://www.rstudio.com/products/rstudio/download/).

Copy and paste these commands into the RStudio console. If this is the first time you've used R you'll be asked to choose a CRAN mirror. Use the *US (CA-1) https mirror.* This will install the required packages for the app.

```r
install.packages("leaflet")
install.packages("DT")
install.packages("data.table")
install.packages("shiny")
install.packages("shinyjs")
install.packages("ggplot2")
install.packages("lubridate")
install.packages("dplyr")
install.packages("sp")
install.packages("geojsonio")
install.packages("adehabitatHR")
install.packages("gridExtra")
install.packages("fasttime")
```

I tried, for a long time to limit the number of packages required for the application. However, as more functionality is included in the application, more packages are required to do all the analyses.

To run the app use the command below. For all future uses this is the only line you will need to run.
```r
shiny::runGitHub("CollarDataExport", "mgritts", launch.browser = TRUE)
```

Permissions for the GIS data drive (V:/ActiveProjects/Game) is required to access the data for the application.

## Instructions

General Instructions for the use of the application. If you want a more general introduction to R use the [Quick R website](http://www.statmethods.net). For additional analysis or visualizations in R contact Mitch Gritts.

### Collared Animals Tab

The application opens with a table of animals collared with GPS collars. The table can be filtered using the *Species* and *Management Area* drop down lists. The *Management Area* drop down only filters the table for Mule Deer.

Any field in the table can be searched using the search bar on the right. The table can be sorted by clicking the arrows next to each column name.

### Spatial Tab

The map shows every collar location. A BBMM 95% utilization distribution can be estimated by clicking the Estimate BBMM checkbox. This functionality is only supported for one animal at a time.

### Movement Tab

This tab can be used to plot several parameters related to animal movement. There are 4 figures for visualizing GPS data. These include a cumulative distance (sig.dist), net squared displacement (R2n), distance, and a histogram of distances. Refer to [Bunnefeld et al. 2010](http://onlinelibrary.wiley.com/doi/10.1111/j.1365-2656.2010.01776.x/full) for more information on NSD calculations and utility.

The map below shows every collar location. A BBMM 95% utilization distribution can be estimated by clicking the Run BBMM checkbox. This functionality is only supported for one animal at a time.

### Data Tab

The fourth page shows all the GPS data for individuals displayed on the map. This includes every GPS fix (not only every 20 as mapped) for the species, management area (for deer), NDOW ID, and date range selected. This data can be downloaded as a .CSV file by clicking the *Download Data* button, and saved to your Downloads folder. The downloaded data will include every GPS location.

## Demo

[View a brief demo here.](https://drive.google.com/file/d/0B1OupsoLNZvkcExIT2VzcUlySWc/view?usp=sharing)

## About the Data

The sources of raw data are the GPS collar manufacturers for each collar. This data is organized and maintained in a relational database by NDOW GIS & Game staff. New collar data is migrated to the database once a month. Therefore, the data in this application isn't the most up to date. At the greatest, the data is delayed by 30 days. The data is stored on NDOW's network, therefore users must be networked to and have permission for the Game folder on the GIS Share drive. This is due to the sensitive nature of location data. This is a temporary solution, we are looking for alternatives that will make the data more accessible to all staff that may use this data.

## Known Bugs

Current version has no known bugs

## TODO
- [ ] Change name of column headers
- [ ] Use 'start' and 'stop' markers for first and last points
- [x] Clear/Reset Map page input
- [ ] Reset input on tab change... may not be possible?
- [ ] Use data.table for all data munging
- [ ] Use Leaflet Draw to allow users to subset based on the area
- [ ] A way for users to request analysis based on data they've entered
- [ ] Remove erroneous points, persistent to data download
- [x] Include migration analysis plots
- [x] Include utilization distributions.
  - [ ] As shapefile?
- [x] NSD plots and associated maps

To add items to the TODO list, or report errors that occur while using the application contact Mitch Gritts (mgritts@ndow.org).
