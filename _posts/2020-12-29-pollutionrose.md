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
In concentric circles going out from the rose's center are marks noting the percentage of the pollutant readings that were taken when the wind direction fell within the angles of one of those wedges. To simplify things for a moment, we can change the "breaks = " parameter to not break the pollutant readings into different bins. This shows us the pollution rose which is essentially just a windrose with no windspeed information. It only shows the percentage of the time for the dataframe where there was a reading for this pollutant and the wind was coming from the direction of that specific wedge. But because we have lumped all the pollutant readings into one bin, it tells us no more details about how different wind directions were contributing to pollutant levels. 
If you add up the percentages of all the wedges, you get 100%. 

[pollution rose image]

Now, if we add our default bins back in, we can see that each wedge is then broken up into the colors of the different pollutant bins. The colors on each wedge show the proportion of readings from that wind direction that fall in particular bins. The color closest to the center represents the lowest concentration readings, and the color furthest out on the rose represents the bin with the highest pollutant concentration. 
In summary, the pollution rose provides us with information on: 1) what percentage of the time the wind is coming from different wind directions and 2) what proportion of each wind direction has readings of each bin of pollution measurements. 

## Arguments 

Lets go through the arguments that pollutionrose() takes. Shown are the defaults. As we said, you'll need to specify your dataframe and probably your pollutant. The rest would be used only if you want to change the defaults. 

***dataframe*** The first argument is your dataset, which should be in the form of a dataframe. This is inputted as just the name of the dataframe, as shown in the above examples. 

***pollutant*** 'pollutant = "nox"' Pollutant specifys which series in your dataframe to use as the pollutant for the pollution rose. 

***key*** 'key = TRUE' You can switch this to false if you don't want the key. 

***key.footer*** 'key.footer = pollutant' Default is that the label at the bottom of the key is the name of the footer. 

***key.position*** 'key.positoin = "right"' You could change this if you hated the key being on the right. 

***breaks*** 'breaks = 6' This specifies the number of bins that the pollutant is broken into. Adjust if you want more or less bins.

***paddle*** 'paddle = FALSE' When paddle is set to FALSE, it makes the pollution rose with wedge shapes like we've shown in the pollutionrose() examples. The paddle = TRUE gives you the shape used as the default in the windrose() example above. 

***seg*** 'seg = 0.9' This specifies the width of the wedge in relation to the size of the angle. The size of each wedge is seg * angle, so you can adjust the seg parameter to give you more or less space between wedges. 

***normalise*** 'normalise = FALSE' If this is changed to TRUE, then each wedge is adjusted so that the percentages shown on the rings add up to one. 

pollutionrose() is a wrapper that uses windrose() function. So here are a few windrose() arguments that might be helpful in adjusting your pollutionrose() plot (This is a selected list. For the full list of arguments, consult the documentation(2)):

***angle*** 'angle = 30' This is what divides the whole rose into wedge angles. So if you want a different number of wedges (and thus having each wedge capture more or less wind angles), you can adjust this angle. Ideally, have it be a factor of 360. 

***type*** 'type = "default"' The default provides a single plot like we've seen in our examples. Alternative settings will divide plots by different groupings. Options include: year, hour, month, season, weekday, monthyear

***statistic*** 'statistic = "prop.count"' The default for statistic is "prop.count", which sizes the bins of the wedges based on their proportion of the measurements. By changing to statistic = "prop.mean", you can instead see the wedge bins sized based on their contribution to the mean. If for some reason you wanted the wedges to show actually counts of the measurements in each bin, then statistic = "abs.count" would provide that. 






(1)Carslaw, D. C. and K. Ropkins, (2012) openair --- an R package for air quality data analysis. Environmental Modelling & Software. Volume 27-28, 52-61.
(2)https://davidcarslaw.github.io/openair/reference/windRose.html#references
