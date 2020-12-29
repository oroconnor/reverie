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
windrose() needs two properly identified columns in your data in order to function: 1) a windspeed column, labelled "ws" and 2) a wind direction column labelled "wd." If these columns are not labelled this way in your dataframe, you can specify which columns that windrose() should use in your arguments, by identifying your column names using "ws = " and "wd = ":

```r
windrose(dataframename, ws = "actualwindsppedcolumnname", wd = "actualwinddirectioncolumnname")
```





(1)Carslaw, D. C. and K. Ropkins, (2012) openair --- an R package for air quality data analysis. Environmental Modelling & Software. Volume 27-28, 52-61.
