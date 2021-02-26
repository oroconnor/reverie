---
layout: post
title:  EDA - Summaries and First Looks
categories: [R]
---

What do you do as the first steps to explore your data? If you know very little about your new dataset, or are looking for where to start exploring, what are some places to begin your exploration? 

We're going to look at a few packages and functions that can be called easily to give you that first glimpse into your data. At this point in the process, the goal is get a sense of the basic summary statistics, the rough distribution of your variables, and a first look at the relationships between different variables. After taking a peak at your data in this way, you will establish your own bespoke next steps for diving deeper into you data. You'll almost certainly want to plot variables on their own so that you can set up graphs of the variable to be more interpretable. Our focus in this article will be on quick snapshots that gives us a first look at all the variables. 

While this information is broadly applicable, there are few important considerations to keep in mind. For the most part, most of these functions are designed to work with numeric data. A few of the functions will operate with other data types in the dataframe, such as character, but many just won't do anything unless the columns in the dataframe are all numeric. Converting the character variable to a factor (if it is, in fact, some sort of categorical variable) will allow a few of the functions to excecute, but won't yield any valuable information. For the functions below, it's best to select just your numeric data to work with, and exclude datetime or character variables. The important exception is summaryPlot(), which actually requires the datetime variable because it is meant for accessing time-series data and creates its plots using time as the x axis. 

Let's start by looking at some non-graphical ways to take a peak at your data one variable at a time, then look at graphical representations of your single variables. Finally, we will look at representations of pair-wise relationships between your variables. 

## Summary Statistics

Let's just load all the packages we're going to need. Life is short. 
```r
library(tidyverse)
library(PerformanceAnalytics)
library(car)
library(psych)
library(pastecs)
library(openair)
library(corrplot)
```

You've loaded your data into R and transformed it into a dataframe. Time to take a look and see what we've got here. 

```r
#loading the data into a dataframe
#in my case, I'm loading a dataframe with air quality monitoring data
#again, select a subset of your data that contains only the numeric columns
df <- as.data.frame(whateverTheDataSourceIs)


#now we can take a look at the look at the data
str(df)
```

<img src = "https://oroconnor.github.io/td/images/summary/str.png" alt = "str() function">

An alternative to base R's str() is the tidyverse's glimpse(), which is pretty similar. While there are distinctions, from both calls we get the number of rows in our datatframe, a list of the variables, the data type of each variable, and a sample of the first rows of the dataframe. 

Now lets use the base R summary() to get some basic summary statistics for each variable. As you can see, it shows us minimum and maximum, quartiles, mean and median, broken out by variable. 

```r
summary(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/summary.png" alt = "summary() function">

Super helpful. 

By calling the psych package's describe() function, we can see the summary statistics organized in (I think) a more readable table format that makes it easier to compare between the different variables. We also add in a few extra summary statistics: number of observations, standard deviation, a trimmed mean (trimmed - trims 10% off the top and bottom by default), maximum absolute deviation (mad), range, skew, kurtosis, and standard error. 

```r
describe(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/describe.png" alt = "describe() function">

Another, fairly similarly formatted option, sta.desc() from the pastecs package, adds in yet another couple of summary statistics. I think that it's particularly useful to get the number of null and NA values in there. 

```r
stat.desc(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/stat.desc.png" alt = "stat.desc() function">

## Univariate Plots

We got a sense of the data types of our variables as inputted, and we were able to take a look at some basic summary statistics about each variable. So we have some information in hand that tells us some about the central tendencies of our variables, as well as their dispersion. But it would be helpful to get a visual look at each variable in order to get a sense of their distribution, as well as see where data is missing and maybe which variables have outliers that might even obstruct a good luck at the distribution of the rest of the data. Again, ultimately you will need to plot each variable of interest to be able to better control the scale and to drill down into investigating any issues that you uncover with that variable. For now, we're focusing on quick ways to take a first pass and get a big picture of your dataset. 

One of my favorite functions to use for this purpose with time series data is the summaryPlot() function in the openair package. It provides a time series look at each variable, which helps to visualize both how the data is changing over time, and highlights missing data. There is a bar underneath the plot for each variable that shows where the NA datapoints are. There are also a few summary statistics given. On the right, you can see a simple histogram for each variable and have a sense of the distribution. For some variables, this will be fairly informative. For others, the bin size or scale won't be too helpful and you'll need to follow up with making individual histogram plots of the variable. As an alternative, you can set these plots to be density plots by including the argument 'type = "density plot"'. 

```r
summaryPlot(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/summaryPlot.png" alt = "summaryPlot() function">

It is important to note that summaryPlot() needs a column labelled "date" in order to work. I'm not sure what all the possible formats it will accept that column as, but I've had success using a datetime data type and labelling the column "date" before calling summaryPlot(). summaryPlot() only takes numeric or integer variable types. 

Most of the bivariate plots we're going to look at also show density plots or histograms for the individual variables, so let's move on to discussing those.


## Bivariate Plots

Another nice things to be able to see when first exploring your dataset is how the variables relate to each other. Each of the next three functions provide a matrix of plots scatterplots of each pair of variables plotted against each other. 

The first one I'll show is scatterplotMatrix() from the car package. On the diagonal, it provides density plots and variable names. The plots on either side of the diagonal are redundant bivariate scatterplots with fitted lines. 

```r
scatterplotMatrix(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/scatterplotmatrix.png" alt = "scatterplotMatrix() function">

Honestly, we can move past that one pretty quickly because I find this next one to be cleaner and more useful. chart.Correlation(df) from the package PerformanceAnalytics has similar bivariate plots, has histograms and density plots on the diagonal, and provides us with correlation coefficients. The asterisks with the correlation coefficients indicate significance levels as calculated by the cor.test function. I mean, so much usefull information is packed into this function that is really easy to call. Wow!

```r
chart.Correlation(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/chart.Correlation.png" alt = "chart.Correlation() function">

The pairs.panels() function from the psych package is very similar to the above chart.Correlation. It has some different defaults (for example, it does not show the asterisks significance levels and does show correlation ellipses by default), but both functions can be adjusted using their arguments to turn these features on or off to your liking. 

```r
pairs.panels(df)
```
<img src = "https://oroconnor.github.io/td/images/summary/pairs.panels.png" alt = "pairs.panels() function">

Both pairs.panels() and chart.Correlation() show a smoothed line by default, but they can adjusted to show a fitted line, or to add confidence intervals to the lines if you wish. 


The last bivariate plot function that I'd like to highlight is the corrplot() function from the (you guessed it) corrplot package. The first argument that you pass corrplot() needs to be the results of using the correlation function cor() on your dataframe. For example, the simplest usage might by 
```r
corrplot(cor(df))
```
That will give you the default version, which is using the "circles" method. I'd like to show you the ellipse version first though. 
```r
corrplot(cor(df), method = "ellipse")
```
<img src = "https://oroconnor.github.io/td/images/summary/corrplot.png" alt = "corrplot() function">

As you can see, we've stripped out any visualizations of the actual data and focused on the correlation relationships. The more linear the shape of the ellipse (and the darker the color), the stronger the correlation. 
This package offers a variety of options for your correlation plots, and various ways to tweak them. You can find the details here. https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html

You can explore the "circle", "square", "number", "shade", "color", and "pie" method options.

## Your move next
Now that you've caught a quick look at your data with these easy-to-call functions, it's time to continue your exploratory data analysis in a more thorough way, tailoring your exploration to the specific nature of your data. But hopefully these glimpses into your data helped you learn about what you're dealing with, and gave you some ideas for what to explore. 

If you want to take a look at the code I used for this post, [it's saved here.] (https://github.com/oroconnor/td/blob/master/code/summary.R_)
