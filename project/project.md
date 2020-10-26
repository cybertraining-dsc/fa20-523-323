# Developing a Hotel Price Predictor as a Consumer Tool

Anthony Tugman, [fa20-523-323](https://github.com/cybertraining-dsc/fa20-523-323/), [Edit](https://github.com/cybertraining-dsc/fa20-523-323/blob/master/project/project.md)

{{% pageinfo %}}

## Abstract

Travel for leisure typically allows the traveler flexibility in transportation, accomodation, dining, and activities. A balance must be met between enjoyment and cost, and while some costs are based on the decisions of the traveler others, such as accomodation cost, are influenced by external forces.  In developing the hotel price predictor, these external forces are analyzed for their weight on price.  As a result, a demonstration of a consumer tool will be produced.


Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** travel, finance, hospitality, tourism

## 1. Introduction

To demonstrate a working knowledge of machine learning on big data, as well as to contribute discussion to big data applications in the tourism industry, a hotel price predictor will be attempted. Using a variety of features that describe in detail a series of hotel stays over the previous 3 years, linear regression will be used to predict hotel price trends over the course of a year. Hotel prices are dependent on many factors, so it may be necessary to create an interactive model so the user can view personalized predictions for their specific needs.  

## 2. Background Research and Previous Work  
Various "hobby-level" hotel price calculators have been attempted and posted online for review.  These price calculators are based on limited datasets and are limited in the number of features considered. A limited dataset makes it difficult to be confident in the resulting prediction, as the dataset may have been to small to accurately train and test the model.  
## 3. DataSets
The dataset is available from Kagle and is titled hotel_bookings.csv [1].[^first]  This dataset was previously part of a small competition on the site, and because of this has multiple existing contributions.  However, from brief analysis it seems that the application of linear regression to user specific requirements is novel.  Atributes of the data set collected after analysis:  
* Shape (119390,32)
* Shape w/ duplicates removed (87396,32)
* Three categories contain null values (country,agent, and company)  
  
Country describes the origin of the traveler, agent describes the ID of the travel agency, and company describes the ID of the company paying for the trip.  These factors do not make significant contributions to the price of a hotel room and were included for administrative purposes.  As a result, these categories will be removed entirely.  Further analysis shows that although the number of babies as guests was tracked, no travlers had babies so this category may be removed. Aditionally "days in waiting list can be removed" as it is also not useful for this purpose.  Therefore, the final data set:  
*Shape (87396,27)
The size of the data set has not been established, but it contains 3 years worth of data on two flavors of hotel (city and resort).  Along with each reservation is 38 attributes that give more detail into how the average daily rate was arrived at.  Further dataset analysis must be completed to determine which of the 38 attributes are of interest.  This section will continue to be updated. 


## 3. Methodology/Process

The dataset is imported directly from Kaggle into Python for analysis.  This analysis will lead to determination of what attributes will be useful for the prediction.  After the algorithim is initially run, it will be confirmed/improved for accuracy.  Additionally, patterns will be evaluated to determine if other useful insights may be revealed.  Based on which patterns and trends are determined, the interactive user input acceptance may be added.  The following process will be followed:  
*  Import data from Kaggle into Pandas for analysis
*  Clean data and determine important attributes
*  Split training/test data
*  Linear Regression
*  Results Evaluation
*  User Input
## 4. Technologies Used
* Python
* Google Collab
* Pandas
* Scikit-learn










## 5. References
[^first]: "Hotel booking demand", Kaggle.com, 2020. [Online]. Available: https://www.kaggle.com/jessemostipak/hotel-booking-demand. [Accessed: 17- Oct- 2020].