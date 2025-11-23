# outages-analysis---USA

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