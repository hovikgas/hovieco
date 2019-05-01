#  Restaurant Development in Los Angeles

---

### Problem Statement


The Hovies Consulting group represents the LA Chamber of Commerce. They have contracted us to analyze whether there is a relationship between property values and the types of restaurants in a community (based on price & food type). With this investigation we want to be able to advise entrepreneurs and restauranteurs on potential areas to expand their businesses. By understanding the affluence of a given community, in addition to the price point and concentration of restaurants in that area, entrepreneurs will be able to make informed choices about where to open/expand their businesses. To answer these questions, we'll rely on LA restaurant data obtained via the Yelp API and publicly available housing data from the LA County Accessor’s office. From the LACC perspective, understanding the types of restaurants in various communities will be among the many factors that are considered when promoting businesses throughout the Los Angeles area.

Primary questions of interest include:

- Is there a relationship between home values and Yelp restaurant meta data?
- Which restaurant attributes are most predictive of median home values in a given locality?
- Can we visually explore the concentration of restaurants (based on price and type) in a given locality?

---

### Executive Summary

This analysis starts off by collecting data from Yelp and the Los Angeles County Assessor's Office for restaurants and home values in Los Angeles, respectively. Numerous models were run, ranging from simple linear regression to Random Forests regression. we started off with grouping the data by zip codes (103 Los Angeles zip codes). We then created our 103 of our own clusters, against which to compare our baseline models. 

## Clustering methodology and Final Model Results
KMeans clustering  utilized as the Unsupervised model to cluster homes and restaurants together based off latitude and longitude cooridinates. KMeans did a better job than HDBScan in creating homogeneous clusters (HDBScan was leaving ~30% of properties as unclassified).

The final production model used was based on Ridge Regression, and its Root Mean Squared Error (RMSE) was $208,000. This model was overfit along with all the other models but scored highest on the test set (unseen data) at R-Squared of 0.65.

Our model predicted prices of home clusters on the lower end of the price range better than more expensive home clusters. We had sparse representation of restaurants in the more expensive home clusters. If possible, more restaurant information need to be gathered in those neighborhoods.

---

### Data Overview

LA Housing data: Location and home values for 130K homes in the Greater LA area
Yelp Restaurant data: Data for 30K restaurants was collected via the Yelp API (Yelp Data Summary below):

|Feature|Type|Description|
|---|---|---|
|**id**|*string*|unique restaurant id|
|**name**|*string*|restaurant name|
|**type**|*string*|category of restaurant (i.e. Mexican, Chinese, etc)|
|**rating**|*float*|The avg. rating across customer reviews (0.0 - 5.0|
|**review_count**|*int*|The total number of yelp reviews for a given restaurant|
|**price**|*int*|Discrete value representing the cost of dining (1 - 4) 4 = most expensive|
|**zipcode**|*int*|zipcde of the restaurant|
|**latitude**|*float*|latitude coordinates|
|**longitude**|*float*|longitude coordinates|
|**distance_centroid**|*float*|distance from home/restaurant from centroid|

---

### Summary & Next Steps
More robust meta data on restaurants is needed to produce more accurate predictions(i.e. more accurate categories, fast food vs dine-in, etc.). While creating restaurant clusters based on the latitude and longitude did little to improve the model, clustering restaurants based on the proximity to one another may prove to be more helpful. In addition, we'd like to build an interactive web application that allows users to segment the city (based on home values or restaurant price) and see the concentration of restaurants in that area via Heroku. The current visualization is only accessible on the local machine on which it was created.

---

#### Sources
- Dash documentation: https://dash.plot.ly/  
- Plot.ly documentation: https://plot.ly/python/
- LA County Open Data: https://data.lacounty.gov/
- Yelp API Documentation: https://www.yelp.com/developers/documentation/v3
