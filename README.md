# Outages Analysis - USA

# **Introduction**

In this analysis, I explored a dataset which contained the major power outages that has occurred in the mainland United States from January 2000 to July 2016 with a major power outage being defined as an outage that has impacted at least 50,000 customers or caused an unplanned firm load loss of at least 300 MW as defined by the Department of Energy. These customers could include residential, industrial, and commercial customers. Additionally, the dataset also contains information of the characteristics of each state that the major outage occurred in, including but not limited to data such as population of the state when the outage occurred, GSP per capita, and much more. 

One question my project is centered around and is looking to explore further on is **What factors explain why outage durations differ?**

The importance of Understanding what drives long-lasting power outages is critical for several reasons. If grid operators can estimate the likely duration of an outage early on with data before the outage occurs, they can allocate repair crews, equipment, and emergency resources more efficiently. Better allocation leads to faster restoration, reduced economic losses, and improved customer satisfaction. By examining how these factors relate to outage duration, this project aims to identify the key drivers of prolonged outages and build a predictive model that estimates outage length using only the information available at the start of the event.

The number of rows in this dataset is 1534, meaning from January 2000 to July 2016, there have been 1534 recorded major outages in the United States. There are 57 columns total but I will narrow it down to the relevant ones for the purpose of exploring my question.


## **Relevant Columns**

| Column Name           | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `YEAR`                | Year in which the major outage occurred.                                    |
| `U.S._STATE`          | Name of the U.S. state where the outage occurred.                           |
| `CAUSE.CATEGORY`      | Category describing the main cause of the outage in words.                  |
| `DEMAND.LOSS.MW`      | Estimated electricity demand lost during the outage, in megawatts (MW).     |
| `CUSTOMERS.AFFECTED`  | Number of customers who lost power during the outage.                       |
| `CLIMATE.REGION`      | NERC Region involved in the outage.                                         |
| `ANOMALY.LEVEL`       | Temperature anomaly relative to the historical average for that region.     |
| `MONTH`               | Month in which the outage occurred (1–12).                                  |
| `OUTAGE.DURATION`     | Duration of the outage, in minutes.                                         |
| `POPULATION`          | Total population of the state in which the outage occured.                  |
| `POPDEN_URBAN`        | Population density in urban areas of the state (people per square mile).    |
| `POPDEN_RURAL`        | Population density in rural areas of the state (people per square mile).    |
| `AREAPCT_URBAN`       | Percentage of the state’s land area classified as urban.                    |
| `PC.REALGSP.STATE`    | Real Gross State Product per capita (measured in 2009 USD).                 |
| `TOTAL.PRICE`         | Average monthly electricity price in the U.S. state (cents/kilowatt-hour)   |
| `TOTAL.CUSTOMERS`     | Total number of electricity customers in the state.                         |
| `TOTAL.REALGSP`       | Real GSP contributed by all industries (measured in 2009 USD).              |


# **Data Cleaning and Exploratory Data Analysis**

## **Data Cleaning**

1. I started my data cleaning process by creating a copy of the original dataframe, in case If I make any mistakes along the way I can refer back to it again.
2. I then dropped all columns that are irrelevant to my research question and my analysis. The columns I kept are the same columns displayed in the table above.
3. I then drop rows where the ==OUTAGE.DURATION== values are 0 or nan because it is highly implausible for a major outage to be 0 minutes of length. I also drop rows with nan ==OUTAGE.DURATION== values because ==OUTAGE.DURATION== is the variable we are trying to predict in the later steps.
4. Then I convert some columns to their appropiate types as needed. For instance, converting ==PC.REALGSP.STATE== to a column of integer values from string values make sense for easier data manipulation like arithmetics if needed in the future.

|   YEAR | U.S._STATE   | CAUSE.CATEGORY     |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED | CLIMATE.REGION     |   ANOMALY.LEVEL |   MONTH |   OUTAGE.DURATION |   POPULATION |   POPDEN_URBAN |   POPDEN_RURAL |   AREAPCT_URBAN |   PC.REALGSP.STATE |   TOTAL.PRICE |   TOTAL.CUSTOMERS |   TOTAL.REALGSP | DATE                |
|-------:|:-------------|:-------------------|-----------------:|---------------------:|:-------------------|----------------:|--------:|------------------:|-------------:|---------------:|---------------:|----------------:|-------------------:|--------------:|------------------:|----------------:|:--------------------|
|   2011 | Minnesota    | severe weather     |              nan |                70000 | East North Central |            -0.3 |       7 |              3060 |      5348119 |           2279 |           18.2 |            2.14 |              51268 |          9.28 |           2595696 |          274182 | 2011-07-01 00:00:00 |
|   2014 | Minnesota    | intentional attack |              nan |                  nan | East North Central |            -0.1 |       5 |                 1 |      5457125 |           2279 |           18.2 |            2.14 |              53499 |          9.28 |           2640737 |          291955 | 2014-05-01 00:00:00 |
|   2010 | Minnesota    | severe weather     |              nan |                70000 | East North Central |            -1.5 |      10 |              3000 |      5310903 |           2279 |           18.2 |            2.14 |              50447 |          8.15 |           2586905 |          267895 | 2010-10-01 00:00:00 |
|   2012 | Minnesota    | severe weather     |              nan |                68200 | East North Central |            -0.1 |       6 |              2550 |      5380443 |           2279 |           18.2 |            2.14 |              51598 |          9.19 |           2606813 |          277627 | 2012-06-01 00:00:00 |
|   2015 | Minnesota    | severe weather     |              250 |               250000 | East North Central |             1.2 |       7 |              1740 |      5489594 |           2279 |           18.2 |            2.14 |              54431 |         10.43 |           2673531 |          292023 | 2015-07-01 00:00:00 |

## **Exploratory Data Analysis**

**Univariate Analysis**
<iframe
  src="assets/outages-per-year.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This univariate plot shows the count of how much major outages occured across every ==YEAR== from 2000 to 2016. You can observe that the year 2011 has the highest count of major outages across the US at 221 and the year 2000 has the lowest count of major outages at just 12 with most of the major outages concentrated in later years.

**Bivariate Analysis**
<iframe
  src="assets/average-per-category.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This bivariate plot shows the average ==OUTAGE.DURATION== per ==CAUSE.CATEGORY==. We can see that if ==CAUSE.CATEGORY== was fuel supply emergency, it would have the highest average 
==OUTAGE.DURATION== at around 13,484 minutes and if it was islanding, it would have the lowest average ==OUTAGE.DURATION== at around 200 minutes.

