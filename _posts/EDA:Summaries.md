---
layout: post
title:  EDA: Summaries and First Looks
categories: [R][EDA]
---



What do you do to as the first steps to explore your data? If you know very little about your new dataset, or are looking for where to start exploring, what are some places to begin your exploration? 

We're going to look at a few packages and functions that can be called easily to give you that first glimpse into your data. At this point in the process, the goal is get a sense of the basic summary statistics, the rough distribution of your variables, and a first look at the relationships between different variables. After taking a peak at your data in this way, you will establish your own bespoke next steps for diving deeper into you data. You'll almost certainly want to plot variables on their own so that you can set up graphs of the variable to be more interpretable. Our focus in this article will be on quick snapshots that gives us a first look at all the variables. 

While this information is broadly applicable, I'm most interested in air and water data, so we will make sure that we address how dataframes of this sort might work with these functions, and how these packages handle time-series data. 

Let's start by looking at some non-graphical ways to take a peak at your data one variable at a time, then look at graphical representations of your single variables. Finally, we will look representations of pair-wise relationships between your variables. 

## Summary Statistics

You've loaded your data into R and transformed it into a dataframe. Time to take a look and see what we've got here. 

```r
#loading the data into a dataframe
df <- as.dataframe(df)

#now we can take a look at the look at the data
str(df)
```

An alternative to base R's str() is the tidyverse's glimpse(), which is pretty similar. While there are distinctions, from both calls we get the number of rows in our datatframe, a list of the variables, the data type of each variable, and a sample of the first rows of the dataframe. 
