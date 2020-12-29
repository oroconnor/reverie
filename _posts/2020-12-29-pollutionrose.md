---
layout: post
title:  Pollution Rose Function in Openair Package
categories: [R]
---


The **openair** R package, by Carslaw and Ropkins, provides a simple way to create a pollution rose from air quality and weather data (1). We're going to look at what this function of the package can do, and the mechanics of how to best take advantage of it. 

[pollution rose image]

## openair

**openair** is an R package created by David Carslaw and Karl Ropkins that seeks to provide tools for analysis of air pollution data. Developed in the UK, it is now used widely throughout the world for the importing, trend analysis and visualization of air quality data. **openair** is an open source package under the GLP >=2 license, and the developers chose to create their tools with R, and open source language, in order to promote reproducability, transparency, and shared methodologies in the atmospheric sciences (1).

## pollutionrose()

pollutionrose() is a function in the openair package that builds on the windrose() function in order to create a visualization showing the relationship between wind direction and air pollution time series data. In its simplest form, windrose() takes your weather dataframe as its only required argument:

```r
windrose(dataframename)
```
[wind rose image]

windrose() needs two properly identified columns in your data in order to function: 1) a windspeed column, labelled "ws" and 2) a wind direction column labelled "wd." If these columns are not labelled this way in your dataframe, you can specify which columns that windrose() should use in your arguments, by identifying your column names using "ws = " and "wd = ":

```r
windrose(dataframename, ws = "actualwindspeedcolumnname", wd = "actualwinddirectioncolumnname")
```

windrose() displays "Frequency of Counts by Wind Direction." In this case, the "counts" are of windspeed measurements that fall into different bins of windspeed ranges. pollutionrose() also creates a visualization showing "Frequency of Counts by Wind Direction." However, with pollutionrose(), the "counts" are measurements of a certain pollutant, again seperated into bins. 

The pollutionrose chart shows how different wind directions contribute to the counts of this particular pollutant, as broken down into ranges. 

[pollution rose image]

## pollutionrose() basics

So the pollutionrose() function, like windrose(), takes your dataframe as its first argument. Much like windrose(), if your wind direction column name is already named "wd", then you won't need to specify it in the arguments. Otherwise you will need to clarify the name of your wind direction column with "wd = ". 
The other parameter that pollutionrose() needs is the name of the pollutant column of your dataset. pollutionrose() has the default pollutant name as "nox". So if your column is named "nox", then you are all set. Otherwise, you will need to specify the name of the label of the pollutant column with the argument "pollutant = ". So while theoretically, the most simple deployment of pollutionrose() is:

```r
pollutionrose(dataframename)
```
More often than not, you will need to clarify either the wind direction column name or the pollutant, so in practice the simplist use of pollutionrose() looks like this:

```r
pollutionrose(dataframename, pollutant = "actualpollutantcolumnname" wd = "actualwinddirectioncolumnname")
```

## Interpretation

What are we seeing when we look at a pollutionrose chart? By default, you'll see a key on the right of the chart. This shows the different ranges that the function is using to bin the pollutant measurements, as well as a label for the choosen pollutant. 
In the rose itself, there are wedges that represent the different wind directions for that site. By default, it will use windrose()'s deafult of 30degs for each wedge. 
In concentric circles going out from the rose's center are marks noting the percentage of the pollutant readings that were taken when the wind direction fell within the angles of one of those wedges. To simplify things for a moment, we can change the "breaks = " parameter to not break the pollutant readings into different bins. This shows us the pollution rose which is essentially just a windrose. It only shows the percentage of the time for the dataframe where there was a reading for this pollutant and the wind was coming from the direction of that specific wedge. But because we have lumped all the pollutant readings into one bin, it tells us no more details about how differnt wind directions were contributing to pollutant levels. 

[pollution rose image]

Now, if we add our default bins back in, we can see that each wedge is then broken up into the colors of the different pollutant bins. The colors on each wedge show the proportion of readings from that wind direction that fall in particular bins. The color closest to the center represents the lowest concentration readings, and the color furthest out on the rose represents the bin with the highest pollutant concentration. 




(1)Carslaw, D. C. and K. Ropkins, (2012) openair --- an R package for air quality data analysis. Environmental Modelling & Software. Volume 27-28, 52-61.
