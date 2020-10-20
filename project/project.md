# Predicting Hotel Prices Using Linear Regression

- [ ] abstracts can not have citations

Anthony Tugman, [fa20-523-323](https://github.com/cybertraining-dsc/fa20-523-323/), [Edit](https://github.com/cybertraining-dsc/fa20-523-323/blob/master/project/project.md)

{{% pageinfo %}}

## Abstract

In 2019 the United States hotel industry experienced its tenth consecutive year of growth.  Prior to Covid-19 placing a halt on the country's travel plans, overall occupancy in 2020 was projected to outpace room availability by 1.9% [1].[^first] With an economic recovery inevitable and the law of supply and demand in effect, we set out to develop a hotel price calculator.  Abstract will be updated further at report conclusion.

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** travel, finance, hospitality, tourism

## 1. Introduction

To demonstrate a working knowledge of machine learning on big data, as well as to contribute discussion to big data applications in the tourism industry, a hotel price predictor will be attempted. Using a variety of features that describe in detail a series of hotel stays over the previous 3 years, linear regression will be used to predict hotel price trends over the course of a year. Hotel prices are dependent on many factors, so it may be necessary to create an interactive model so the user can view personalized predictions for their specific needs.
## 2. DataSets
The dataset is available from Kagle and is titled hotel_bookings.csv [2].[^second]  This dataset was previously part of a small competition on the site, and because of this has multiple existing contributions.  However, from brief analysis it seems that the application of linear regression to user specific requirements is novel.  Atributes of the data set collected after analysis:  
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

[^first]: "U.S. Hotel Occupancy Projected to Hit New Record in 2019 Despite Recent Softness", Skift, 2020. [Online]. Available: https://skift.com/2018/11/29/u-s-hotel-occupancy-projected-to-hit-new-record-in-2019-despite-recent-softness/#:~:text=CBRE%2C%20a%20real%20estate%20and,supply%20increase%20of%201.9%20percent. [Accessed: 17- Oct- 2020].

[^second]: "Hotel booking demand", Kaggle.com, 2020. [Online]. Available: https://www.kaggle.com/jessemostipak/hotel-booking-demand. [Accessed: 17- Oct- 2020].
