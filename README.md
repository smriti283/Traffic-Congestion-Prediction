# Traffic Congestion Analysis and Prediction in NYC 


## Overview 

Over the years New York City has been experiencing more and more road traffic congestion, impacting the lives of New Yorkers severely not only with respect to ease of mobility but also in terms of increased air pollution as well as social/ psychological well being. While traffic flow has complex spatial and temporal dependencies, traffic volume remains a key measurable indicator of congestion. Monitoring and predicting the traffic volume within a given road segment or network over a given timeframe can thus help better manage the urban congestion problem, and also prove useful for other urban applications such as city planning, rezoning, urban development, maintenance of roads and environmental concerns, to name a few. 

To address the above, the roadbed segments in NYC first need to be segregated into different ranges of vehicular volumes they experience on a day to day basis, by clustering the roads that display similar trends. The lack of data labels make this an unsupervised learning problem, and can be solved by implementation of K-means clustering, which is simple and easy to implement.

It must also be noted that high vehicular volume on a given road at a given time can also be caused by several other factors, few of which are the width and length of the street, presence of bike lanes, designation as a truck route etc. In the absence of vehicle volume data (which is very commonly encountered in existing datasets), a robust technique is required to classify a given road segment by traffic volume categories. To demonstrate this possibility, supervised learning techniques such as Decision Trees or Random Forests can be trained on the results obtained from clustering. Decision trees are easy to interpret and implement while Random Forests help reduce the overfitting issue encountered in Decision Trees. 

Lastly, based on the above results, the zones or segments that need the most attention can be identified and predictions on hourly and daily volumes can be made. The Hidden Markov Model predictor can be used to achieve this, which takes sequential historical data to predict future observations. Such predictions can help the traffic management authorities to plan for congestion in areas that require the most intervention, and solutions such as street parking adjustment or one-way flow can be implemented for the given timeframe.


## Datasets

- [NYC Traffic Volume Counts (2014 - 2019)](https://data.cityofnewyork.us/Transportation/Traffic-Volume-Counts-2014-2019-/ertz-hr4r) - NYC Open Data
- [NYC Traffic Volume Counts (2012 - 2013)](https://www.kaggle.com/new-york-city/ny-traffic-volume-counts-2012-2013) - Kaggle 
- [LION Shapefile](https://www1.nyc.gov/site/planning/data-maps/open-data/dwn-lion.page) - NYC Department of City Planning
- [NYC Zip Codes shapefile ](https://raw.githubusercontent.com/CUSP2020PUI/Data/master/NY.geojson)


## Methods

1. Initial Data Cleaning and Preprocessing
2. Clustering NYC road segments by vehicular volume using K-Means Clustering Analysis
3. Training the Decision Tree and Random Forests classifier for NYC road network classification in absence of volume counts
4. Predicting traffic volume by hour and day using Hidden Markov Model (HMM) Predictor


## Results

### 1. Initial Data Cleaning and Preprocessing

We started with merging the traffic volume dataset with the LION shapefile (on Segment ID). We then pre-processed the dataset to achieve street nomenclature homogeneity; grouped by roadways; calextracted the day of week; categorized the dataset into Weekday and Weekend records and calculated mean values for hourly traffic. To address the outliers, we cleaned the merged dataset to create 2 separate datasets: one with 8 and more records per segment and the other with 10 and more records per segment. These were further processed to suit the needs of all machine learning algorithms applied. 

### 2. K-means Clustering Analysis of NYC road segments based on vehicle volumes

We found that for Weekdays, the cluster with highest traffic volume (label 1) have two peak time periods: 7AM - 8AM and 3PM - 7PM and for Weekends, the most amount of vehicle volume is observed between 2PM - 5PM.

#### Weekday:


<img width="598" alt="Screen Shot 2023-02-14 at 12 38 19 PM" src="https://user-images.githubusercontent.com/78453405/218857519-7ebe6ee3-6837-426b-bc0c-613182a7c194.png">


#### Weekend:





