---
layout: post
title:  Kingston Home Sales Trends
categories: []
---


Here where I live in Kingston, NY, there is a sense right now that homes are being bought up rather quickly as people in New York City are realizing that a population density of 26,403 per sq. mile isn't as fun during a pandemic.[1] 

You'll hear anecdotes from people looking for a first home of having their offers beaten by quick and high cash offers from New York City buyers. You don't need a dataset to get the general feeling that more people from Brooklyn are moving to Kingston, or at least spending more time in their second homes here while the pandemic is going on. But hearing people chatting about this has gotten me curious to see what kind of impact this trend is having on the home sales for our city. 

\[August 13th update: For examples of the sorts of anecdotes I'm talking about, check out this article that came out a few days after I put this post up... [www.bloomberg.com article](https://www.bloomberg.com/news/articles/2020-08-12/catskills-town-leads-u-s-in-rising-home-prices-with-nyc-exodus)\]

Realtor.com is kind enough to make their real estate transactions data available at [https://www.realtor.com/research/data/](https://www.realtor.com/research/data/)
I've started to pull out and organize some of Kingston's information to see how this year's trends are comparing to previous years'.

The documentation at https://www.realtor.com/research/data/ says that the data is updated at the beginning of the month with the previous months data. So this should be an accurate snapshot of what has happened through July. 


<img src="https://oroconnor.github.io/td/images/kingstondata_1.jpg">


Looking at the four years of information on the Median Listing Price for Kingston, we can see that in July 2020 the Median Listing Price is up from last year, but is also not high in comparison with 2018. We're only looking at Julys because there is a strong seasonality to these metrics, as we will see in a minute.

The Median Days on the Market shows a decline, so houses are moving faster this July than in previous Julys. Now, we don't have longterm data to look at here, so we're only seeing the past four years. But that's really what's most relevant to the question we are asking... what kind of effect the post-pandemic wave of interest is having on Kingston in comparison to what home sales were like pre-pandemic. Certainly homes are on the market for less time this July, but let's add a little context. 

<img src="https://oroconnor.github.io/td/images/kingstondata_2.jpg">

Looking at how the Median Days On The Market changes over the year for the past four years (January through July) shows that this metric experiences a seasonal effect. Home sales slow in the winter months and speed up in the Spring and Summer. This year, 2020, we can see an uncharacteristic slow down in the Spring. One can guess that this abnormal spike in the median days on the market was because of the disruption of the pandemic and the shut-down. By July, the median days on the market has shortened and come back in line with the general trend of the summer from previous years, and in fact has overshot some and and is lower than previous Julys. 

Now, the question is whether the Median Days On The Market is just normalizing and the rest of the year will be similar to previous years, or whether this speed up of the market will intensify or hang on unusually far into the fall and winter. 
Here's the chart with the rest of months filled in. August's data and beyond will show us whether the market falls back in line with the recent seasonal patterns, or continues with an period of abnormally quick home sales. 

<img src="https://oroconnor.github.io/td/images/kingstondata_3.jpg">

I will post an update in early September when we get August's data. In the meantime, I'll poke around and explore more of the information that realtor.com's dataset provides about Kingston. Stay tuned!




You can check out the python code that organized the data and created the charts [here.](https://oroconnor.github.io/td/kingston-homes-code/)



\[August 13th update: Just one quick comment on the Bloomberg article linked to above....
The article compares 2019 second quarter to the same 2020 quarter, and highlights the 18% increase to $276,000 for a "typical selling price". I just want to add a little more context so we can how this fits in with the rest of the data for the past four years. Here's a chart of the monthly Median Listing Price for 2017-2020. I marked dotted lines to show where $276,000 is on the chart, as well as $233,896 (which would be the amount before an 18% increase). Now, this is a little bit apples to oranges, because Bloomberg is talking about selling prices, and this data is for Median Listing Price. 
No doubt, the Median Listing Price has seen a significant increase since the start of 2017. It's illuminating, though, to see that Kingston is not so far off from summer of 2018. 
<img src="https://oroconnor.github.io/td/images/kingstondata_4.jpg">
\]








[1]: https://en.wikipedia.org/wiki/Demographics_of_New_York_City
