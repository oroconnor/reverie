---
layout: post
title:  Reproduceable code for "Kingston Home Sales Trends"
categories: []
---

Again the data for the visualizations in "Kingston Home Sales Trends" are from Realtor.com 
They request that this link be provided with attribution: https://www.realtor.com/research/data/

Here's the reproduceable code that takes the realtor.com dataset and creates the visualizations used in the post:



```python
import pandas as pd
from datetime import datetime as dt
import matplotlib.pyplot as plt

#read the realtor.com data into a pandas dataframe
df = pd.read_csv("/Users/owenoconnor/Documents/scripts/realtor/RDC_Inventory_Hotness_Metrics_Zip_History.csv")

#convert the string dates into datetime objects, and then setting that column as the index for the dataframe.
df["date_dt"]  = pd.to_datetime(df["month_date_yyyymm"], format = "%Y%m", errors = "coerce") 
df.index = df["date_dt"]

kingston = df[df["postal_code"] == 12401]
kingston_subset = kingston[['hotness_score','median_days_on_market','median_listing_price']]
kingston_subset["month"]=kingston_subset.index.month #adds a month column that we can use to sort by
```
