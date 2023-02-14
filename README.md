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


<img width="835" alt="Screen Shot 2023-02-14 at 12 56 29 PM" src="https://user-images.githubusercontent.com/78453405/218861528-6f38a460-9522-464d-bd84-4f9fe56945ac.png">


Further, the clustered road segments were geoplotted for better data representation. Figure 2.3 and Figure 2.4 show spatial distribution of weekdays and weekends clusters: red color indicates high traffic volume segments, blue color indicates medium traffic, and yellow means low traffic. Figure 2.5 shows distribution of roads with highest vehicle volume (i.e. roads clustered under label 1) on both weekdays and weekends. Most of the segments overlap, and these areas need the most attention from traffic authorities to prevent congestion and traffic accidents.


<img width="828" alt="Screen Shot 2023-02-14 at 12 55 53 PM" src="https://user-images.githubusercontent.com/78453405/218861601-43818676-9fed-41a5-aec4-1a7eac963f37.png">

<img width="485" alt="Screen Shot 2023-02-14 at 12 57 02 PM" src="https://user-images.githubusercontent.com/78453405/218861657-e7568d3d-67d1-408a-8713-553a6801bcf8.png">



### 3. Classification of NYC road segments using Decision Tree & Random Forests in absence of volume counts

We visualized a simple decision tree with max_depth = 2 learned from the dataset (Figure 2.6 & Figure 2.7). Using this, if there is a road with variables such as street width, length, truck_ route etc., we can predict which cluster it will belong to even if the vehicular volume data is not available. In both weekend and weekday results, out of sample accuracies of decision tree are slightly better than those of random forest (Table 2.1). In this case, the result from the decision tree model has a higher accuracy than random forests. In terms of both accuracy and interpretability, decision trees are better than random forests at this time. Using a decision tree, we can see the attributes values and how to divide each group into small groups based on specific features.






### 4. Gaussian Hidden Markov Model predictions of vehicular volume

The following results were obtained from the Gaussian HMM for predictions on vehicle volume by the hours considered, and daily vehicle volumes: 


<img width="561" alt="Screen Shot 2023-02-14 at 12 51 35 PM" src="https://user-images.githubusercontent.com/78453405/218860807-3008741f-7316-438e-84ca-66ee1aaa134c.png">


<img width="570" alt="Screen Shot 2023-02-14 at 12 53 34 PM" src="https://user-images.githubusercontent.com/78453405/218860924-ea4aac5c-f2ce-44c8-8ee7-1db5dbc7c0ee.png">



## Conclusion

We used three methods to analyze and estimate traffic volume in NYC; K-Means clustering for clustering the unlabelled data; Decision Tree/ Random Forest for classifying low, medium and high traffic volume areas; and the Gaussian HMM predictor for traffic volume prediction on a given hour and day. With clustering analysis, we analyzed the hourly trends of weekends and weekdays traffic volumes. With Decision tree/ random forest models, we can classify even segments without hourly traffic volumes data into three categories and with the HMM predictor, we predicted the traffic volume for a given timeframe. As a limitation to the HMM model, more open data sets on the target road can lead to better accuracy in traffic volume prediction. 

Nevertheless, the implementation of these approaches demonstrate that for broad level traffic volume analysis and prediction, it is possible to use simple and interpretable machine learning techniques successfully. This can help transportation departments and planners to manage urban traffic by providing solutions such as: 

- Suggesting zones where intervention may be required for traffic management.
- Predicting traffic volumes with road’s attributes for better urban planning/ rezoning. 
- Planning for proper road width and simulating it based on this prediction.
- Suggesting establishment of one-way rules or street parking restrictions based on hourly traffic prediction. 


