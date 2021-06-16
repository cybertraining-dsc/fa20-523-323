---
date: 2021-03-15
title:  Predicting Hotel Reservation Cancellation Rates
linkTitle: Hotel reservations
tags: ["project", "ai", "finance"]
description: "As a result of the Covid-19 pandemic all segments of the travel industry face financial struggle. The lodging segment, in particular, has had the financial records scrutinized revealing a glaring problem. Since the beginning of 2019, the lodging segment has seen reservation cancellation rates near 40%. At the directive of business and marketing experts, hotels have previously attempted to solve the problem through an increased focus on reservation retention, flexible booking policies, and targeted marketing. These attempts did not produce results, and continue to leave rooms un-rented which is detrimental to the bottom line. This document will explain the creation and testing of a novel process to combat the rising cancellation rate. By analyzing reservation data from a nationwide hotel chain, it is hoped that an algorithm may be developed capable of predicting the likeliness that a traveler is to cancel a reservation. The resulting algorithm will be evaluated for accuracy. If the resulting algorithm has a satisfactory accuracy, it would make clear to the hotel industry that the use of big data is key to solving this problem."
author: Anthony Tugman
resources:
- src: "**.{png,jpg}"
  title: "Image #:counter"
---


[![Check Report](https://github.com/cybertraining-dsc/fa20-523-323/workflows/Check%20Report/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-323/actions) 
[![Status](https://github.com/cybertraining-dsc/fa20-523-323/workflows/Status/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-323/actions)
Status: final, Type: Project

Anthony Tugman, [fa20-523-323](https://github.com/cybertraining-dsc/fa20-523-323/), [Edit](https://github.com/cybertraining-dsc/fa20-523-323/blob/main/project/project.md)

{{% pageinfo %}}

## Abstract

As a result of the Covid-19 pandemic all segments of the travel industry face financial struggle. The lodging segment, in particular, has had the financial records scrutinized revealing a glaring problem. Since the beginning of 2019, the lodging segment has seen reservation cancellation rates near 40%. At the directive of business and marketing experts, hotels have previously attempted to solve the problem through an increased focus on reservation retention, flexible booking policies, and targeted marketing. These attempts did not produce results, and continue to leave rooms un-rented which is detrimental to the bottom line. This document will explain the creation and testing of a novel process to combat the rising cancellation rate. By analyzing reservation data from a nationwide hotel chain, it is hoped that an algorithm may be developed capable of predicting the likeliness that a traveler is to cancel a reservation. The resulting algorithm will be evaluated for accuracy. If the resulting algorithm has a satisfactory accuracy, it would make clear to the hotel industry that the use of big data is key to solving this problem.
 
Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** travel, finance, hospitality, tourism, data analysis, environment, big data

## 1. Introduction

Big Data is a term that describes the large volume of data that is collected and stored by a business on a day-to-day basis. While the scale of this data is impressive, what is more interesting is what can be done by analyzing the data [^1]. Becoming more commonplace, companies are beginning to use Big Data to gain advantage in competing, innovating, and capturing customers. It is necessary for businesses to collaborate with Data Scientists to expose patterns and other insights that can be gained from inspection of the data. This collaboration is amongst software engineers, hardware engineers, and Data Scientists who develop powerful machine learning algorithms to efficiently analyze the data. Businesses have multiple benefits to gain from effectively utilizing Big Data including cost savings, time reductions, market condition insights, advertising insights, as well as driving innovation and product development [^1]. 

The lodging industry takes a hit to the bottom line each year as the rate of room reservation cancellations continues to rise. In the instance that a guest cancels a room without adequate notice there are additional expenses the hotel faces to re-market the room as available. If the room is unable to be rented, the hotel loses the revenue [^2]. At the directive of business and marketing experts, hotels have attempted to solve this problem through an increased focus on reservation retention, flexible booking policies, and targeted marketing campaigns. However, even with these efforts, the reservation cancellation rate continues to rise unchecked reaching upwards of 40% in 2019 [^2]. By analyzing the Big Data the lodging industry collects on its customers, it would be possible to form a model capable of predicting whether a customer is likely to cancel a reservation. To develop this model, a large data set was sourced that tracked anonymized reservation information for a chain of hotels over a three-year period. Machine learning techniques will be applied to the data set to form a model capable of producing the aforementioned predictions. If the model proves to be statistically significant, recommendations will be made to the lodging industry as to how the results should be interpreted.

## 2. Background Research and Previous Work

Room reservation completion rates are an important consideration for revenue management in the hotel industry. Unsurprisingly, there have been previous attempts at creating an algorithm capable of predicting room cancellation rates. However, these attempts seem to have taken a more general approach such as predicting cancellations by particular ranges of dates [^3]. Other attempts make broad claims about the accuracy of the resulting algorithm without reliably proving so through statistical analysis [^4]. Most importantly for the scope of this course, these previous attempts use subsets of the full data set available. This has the potential to lead to unpredictability in the performance of the algorithm.

To differentiate from and improve on the attempts previously mentioned, the algorithm produced as a result of the current effort will form a model capable of predicting if a reservation with cancel based on the reservation as a whole, rather than a subset of dates. Not predict the cancellation rate over general stipulations, but rather for a specific customer. Additionally, a special focus will be on proving that the created algorithm is statistically significant and can accurately be extrapolated to larger subsets of the data. Finally, for initial training and testing, larger subsets of the data sets will be utilized due to the increased processing power available from Google Colab. It is important to note that the first-mentioned previous work [^3] appears to use a proprietary data set while the second-mentioned work [^4] appears to utilize the same data set that this study will as well.

## 3. DataSets

Locating a data set appropriate for this task proved to be challenging. Privacy concerns and the desire to keep internal corporate information confidential adds difficulty in locating the necessary data. Ultimately, the following data repository was selected to train and test the reservation cancellation, prediction model:

1. [Hotel Booking Demand](https://www.kaggle.com/jessemostipak/hotel-booking-demand) [^5]

The Hotel Booking Demand data set contains approximately 120,000 unique entries with 32 describing attributes. This data comes from a popular data science website, and previous analysis has occurred. This data set was featured as part of a small contest on the hosting website where the goal was to predict the likelihood of a guest making a reservation based on certain attributes while this study will instead attempt to predict the likelihood that a reservation is canceled. The 32 individual attributes of the data will be evaluated for their weight on the outcome of cancellation. Unlike previously mentioned studies, the attribute describing how the booking was made (in person, online) will be utilized. Researchers believe that the increase in reservations booked through online third-party platforms is contributing to the increase in cancellation [^6]. Considering this attribute may have a significant impact on the overall accuracy of the developed predictive algorithm. Finally, the data set provides information on reservations over the span of a three-year period. During the training and testing phase, an appropriate amount of data will be used from each year to account for trends in cancellations that may have occurred over time. 

|           Attribute           |                          Description                          |
|:------------------------------:|:-------------------------------------------------------------:|
|              hotel             |                  hotel type (resort or city)                  |
|           is_canceled          |              reservation canceled (true/false)              |
|            lead_time           |             number of days between booking and arrival             |
|        arrival_date_year       |                      year of arrival date                     |
|       arrival_date_month       |                     month of arrival date                     |
|    arrival_date_week_number    |              week number of year for arrival date             |
|    arrival_date_day_of_month   |                      day of arrival date                      |
|     stays_in_weekend_nights    |        number of weekend nights (Sat. and Sun.) booked        |
|      stays_in_week_nights      |          number of week nights (Mon. to Fri.) booked          |
|             adults             |                        number of adults                       |
|            children            |                       number of children                      |
|             babies             |                        number of babies                       |
|              meal              |                   meal booked (multiple categories)                  |
|             country            |                       country of origin                       |
|         market_segment         |          market segment (multiple categories)          |
|      distribution_channel      |   booking distribution channel (multiple categories)  |
|        is_repeated_guest       |                 is repeat guest (true/false)                |
|     previous_cancellations     |        number of times customer has canceled previously        |
| previous_bookings_not_canceled |      number of times customer has completed a reservation      |
|       reserved_room_type       |                       reserved room type                      |
|       assigned_room_type       |                       assigned room type                      |
|         booking_changes        | number of changes made to reservation from booking to arrival |
|          deposit_type          |                  deposit made (true/false)                  |
|              agent             |                     ID of the travel agent                    |
|             company            |                       ID of the company                       |
|      days_in_waiting_list      |       how many days customer took to confirm reservation      |
|          customer_type         |        type of customer (multiple categories)       |
|               adr              |                       average daily rate                      |
|   required_car_parking_space   |       number of parking spaces required for reservation       |
|    total_of_special_requests   |                number of special requests made                |
|       reservation_status       |                     status of reservation                     |
|     reservation_status_date    |                  date status was last updated                 |

## 4. Data Preprocessing

The raw data set [^5] is imported directly from Kaggle into a Google Colab notebook [^7].  Data manipulation is handled using Pandas.  Pandas was specifically written for data manipulation and analysis, and will make for a simple process preprocessing the data.  The raw data set must be prepared before a model can be developed from it.  Before preprocessing the data:

* shape: (119390, 32)
* duplicate entries: 31,994 
 
The features of the data set, the categories other than what is being predicted, have varying levels of importance to the predictive model.  By inspection, the following features are removed:
* country: in a format unsuitable for predictive model, unable to convert
* agent: the ID number of the booking agent will not affect reservation outcome
* babies: no reservation had babies
* children: no reservation had children
* company: the ID number of the booking company will not affect reservation outcome
* reservation_status_date: intermediate status of reservation is irrelevant 

In addition, duplicates are removed.  In the case of the features 'reserved_room_type' and 'assigned_room_type' what is of interest is if the guest was given the requested room type.  As the room code system has been anonymized and is proprietary to the brand, it is impossible to make inferences other than this.  To simplify the number of features, a Boolean comparison is performed on 'reserved_room_type' and 'assigned_room_type'.  'reserved_room_type' and 'assigned_room_type' are deleted while the Boolean results are converted to integer values then placed in a new feature category, 'room_correct'.  As it stands, multiple data entries across various features are strings.  In order to build a predictive model, the data entries are converted to integers.

```python
#Convert to numerical values
df = df.replace(['City Hotel', 'HB', 'Online TA', 'TA/TO', 'No Deposit',
                'Transient', 'Check-Out'], '0')
df = df.replace(['Resort Hotel', 'January', 'BB', 'Ofline TA/TO', 'GDS',
                'Non Refund', 'Transient-Party', Canceled'], '1')
df = df.replace(['February', 'SC', 'Groups', 'Refundable', 'Group',
                'No-Show'], '2')
df = df.replace(['March', 'FB', 'Direct', 'Contract'], '3')
df = df.replace(['April', 'Undefined', 'Corporate'], '4')
df = df.replace(['May', 'Complementary'], '5')
df = df.replace(['June', 'Aviation'], '6')
df = df.replace(['July'], '7')
df = df.replace(['August'], '8')
df = df.replace(['September'], '9')
df = df.replace(['October'], '10')
df = df.replace(['November'], '11')
df = df.replace(['December'], '12')
```
After preprocessing the data:
* shape:  (84938, 25)
* duplicate entries:  0

![Data Snapshot](https://github.com/cybertraining-dsc/fa20-523-323/raw/main/project/images/figure1.png)

**Figure 1:** Snapshot of Data Set after Preprocessing 

## 5. Model Creation

To form the predictive model a Random Forest Classifier will be used.  With the use of the sklearn package, the Random Forest Classifier is simple to implement.  The Random Forest Classifier is based on the concept of a decision tree.  A decision tree is a series of yes/no question asked about the data which eventually leads to a predicted class or value [^8].  To start the creation of the model, the data must first be split into a training and testing set.  Typically, this is a ratio that must be adjusted to determine which will result in the higher accuracy.  Here are the accuracy outcomes for various ratios:

| Train/Test Ratio | Accuracy |
|:----------------:|:--------:|
|       80/20      |  77.64%  |
|       70/30      |  77.66%  |
|       60/40      |  79.56%  |
|       50/50      |  77.92%  |
|       40/60      |  75.73%  |
|       30/70      |  74.71%  |
|       20/80      |  73.13%  |

The train/test ratio of 60/40 had the best initial accuracy of 79.56% so this ratio will be used in the creation of the final model.  For the initial test, all remaining features will be used to train the reservation cancellation outcome.  To determine the accuracy of the resulting model, the number of predicted cancellations is compared to the number of actual cancellations.  As the model stands, the accuracy is at 79.56%.
This model relies on 23 features for the prediction.  With this many features it is possible that some features have no effect on the cancellation outcome. It is also possible that some features are so closely related that calculating each individually hinders performance while having little effect on outcome.  To evaluate the importance of features, Pearson's correlation coefficent can be used.  Correlation coefficients are used in statistics to measure how strong the relationship is between two variables.  The calculation formula returns a value between -1 and 1 where a value of 1 indicates a strong positive relationship, -1 indicates a strong negative relationship, and 0 indicates that there is no relationship at all [^9].  Figure 2 shows the correlation between the remaining features.

![Initial Model Correlation](https://github.com/cybertraining-dsc/fa20-523-323/raw/main/project/images/figure2.png)

**Figure 2:** Pearson's Correlation Graph of Remaining Features

In Figure 2 it is straightforward to identify the correlation between the target variable 'is_canceled' and the remaining features.  It does not appear than any variable has a strong positive or negative correlation, returning a value close to positive or negative 1.  There does however appear to be a dominant correlation between 'is_canceled' and three features: 'lead_time', 'adr', and 'room_correct'.  The train/test ratio is again 60/40 and the baseline accuracy of the model is 79.56%.  The remaining features 'lead_time', 'adr', and 'room_correct' are used to develop the new model.  Accuracy is again determined by comparing the number of predicted cancellations to the number of actual cancellations.  The updated model has an accuracy of 85.18%.  Figure 3 shows the correlation between the remaining features.  It is important to note that the relationship between the remaining features and target value does not appear to be strong, however there is a correlation nonetheless.

![Updated Model Correlation](https://github.com/cybertraining-dsc/fa20-523-323/raw/main/project/images/figure3.png)

**Figure 3:** Pearson's Correlation Graph of Updated Remaining Features

As a final visualization, Figure 4 shows a comparison between the predicted and actual cancellation instances.  The graph reveals an interesting pattern, the model is over predicting early in the data set and under predicting as it proceeds through the data set. Further inspection and manipulation of the Random Forest parameters were unable to eliminate this pattern.

![Results Predicted vs. Actual](https://github.com/cybertraining-dsc/fa20-523-323/raw/main/project/images/figure4.png)

**Figure 4:** Model Results Predicted vs. Actual

## 6. Benchmark

To measure program performance in the Google Colab notebook, Cloudmesh Common [^cloudmesh-benchmark] was used to create a benchmark.  In this instance, performance was measured for overall code execution, data loading, preparation of the data, the creation of model one, and the creation of model two.  The most important increase in performance was between the creation of models one and two.  With 23 features, model one took 8.161 seconds to train while model 2, with 3 features, took 7.01 seconds to train.  By reducing the number of features between the two models there is a 5.62% increase in accuracy and a 14.10% decrease in processing time.  Figure 5 provides more insight into the parameters the benchmark tracked and returned.  Additionally, the table provides an analysis of computation time:
| Train/Test Ratio | Accuracy |
|:----------------:|:--------:|
|       80/20      |  77.64%  |
|       70/30      |  77.66%  |
|       60/40      |  79.56%  |
|       50/50      |  77.92%  |
|       40/60      |  75.73%  |
|       30/70      |  74.71%  |
|       20/80      |  73.13%  |
![Benchmark Results](https://github.com/cybertraining-dsc/fa20-523-323/raw/main/project/images/figure5.png)

**Figure 5:** Cloudmesh Benchmark Results

## 7. Conclusion

From the results of the updated predictive model, it is apparent that the lodging industry should invest focus into the Big Data they keep on their customers.  As each hotel chain is unique, it would be necessary for each to develop their own predictive model however it has been demonstrated that such a model would be effective in reducing the number of rooms going unoccupied from reservation cancellation.  As the model is predicting at 85% accuracy, this is a 35% increase in the amount of reservation cancellations that can be accounted for over the current predictive techniques.  To prevent further damage from reservation cancellations the hotel would have theoretically been able to overbook room reservations by 35% or less as they anticipated cancellations.

## 8. References

[^1]: "Big Data - Definition, Importance, Examples & Tools", RDA, 2020. [Online]. Available: <https://www.rd-alliance.org/group/big-data-ig-data-development-ig/wiki/big-data-definition-importance-examples-tools#:~:text=Big%20data%20is%20a%20term,day%2Dto%2Dday%20basis.&text=It's%20what%20organizations%20do%20with,decisions%20and%20strategic%20business%20moves>. [Accessed: 12- Nov- 2020].

[^2]: "Predicting Hotel Booking Cancellations Using Machine Learning - Step by Step Guide with Real Data and Python", Linkedin.com, 2020. [Online]. Available: <https://www.linkedin.com/pulse/u-hotel-booking-cancellations-using-machine-learning-manuel-banza/>. [Accessed: 08- Nov- 2020].

[^3]: "(PDF) Predicting Hotel Booking Cancellation to Decrease Uncertainty and Increase Revenue", ResearchGate, 2020. [Online]. Available: <https://www.researchgate.net/publication/310504011_Predicting_Hotel_Booking_Cancellation_to_Decrease_Uncertainty_and_Increase_Revenue>. [Accessed: 08- Nov- 2020.

[^4]: "Predicting Hotel Cancellations with Machine Learning", Medium, 2020. [Online]. Available: <https://towardsdatascience.com/predicting-hotel-cancellations-with-machine-learning-fa669f93e794>. [Accessed: 08- Nov- 2020].

[^5]: "Hotel booking demand", Kaggle.com, 2020. [Online]. Available: <https://www.kaggle.com/jessemostipak/hotel-booking-demand>. [Accessed: 08- Nov- 2020].

[^6]: "Global Cancellation Rate of Hotel Reservations Reaches 40% on Average", Hospitality Technology, 2020. [Online]. Available: <https://hospitalitytech.com/global-cancellation-rate-hotel-reservations-reaches-40-average>. [Accessed: 08- Nov- 2020].

[^7]: <https://github.com/cybertraining-dsc/fa20-523-323/blob/main/project/colabnotebook/DataAnalysis.ipynb>.

[^8]: "An Implementation and Explanation of the Random Forest in Python", Medium, 2020. [Online]. Available: <https://towardsdatascience.com/an-implementation-and-explanation-of-the-random-forest-in-python-77bf308a9b76>. [Accessed: 12- Nov- 2020].

[^9]: "Correlation Coefficient: Simple Definition, Formula, Easy Calculation Steps", Statistics How To, 2020. [Online]. Available: <https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/>. [Accessed: 12- Nov- 2020].

[^cloudmesh-benchmark]: Gregor von Laszewski, Cloudmesh StopWatch and Benchmark from the Cloudmesh Common Library, <https://github.com/cloudmesh/cloudmesh-common>

