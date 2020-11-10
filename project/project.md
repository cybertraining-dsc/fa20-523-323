# Predicting Hotel Reservation Cancellation Rates

Anthony Tugman, [fa20-523-323](https://github.com/cybertraining-dsc/fa20-523-323/), [Edit](https://github.com/cybertraining-dsc/fa20-523-323/blob/master/project/project.md)

{{% pageinfo %}}

## Abstract

The travel industry is facing unprecedented financial struggle as a result of the Covid-19 pandemic.  Hotels, in particular, are facing financial ruin with cancellations rising leaving rooms to go unrented.  At the directive of business and marketing experts, hotels have been trying to solve the problem through an increased focus on reservation retention, flexible booking policies, and targeted marketing.  Unfortunately, while the Covid-19 pandemic has exacerbated these concerns, cancellations were rising unchecked pre-pandemic as well with industry leaders making similar attempts to solve the problem.  By analyzing reservation data from a nationwide hotel chain it is hoped that an algorithm may be developed capable of predicting the likeliness that a traveler is to cancel a reservation.  The resulting algorithm will be evaluated for accuracy and, if proven, would make clear to the hotel industry that the use of big data is key to solving this problem.

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** travel, finance, hospitality, tourism, data analysis, environment, big data

## 1. Introduction

Artificial Intelligence (AI) is the ability of a machine to perform human-like problem solving and computation at a scale and speed magnitudes larger than what humans are capable of.  Through a cross-disciplinary effort between software engineers, hardware engineers, and data scientists, AI can be taught to perform tasks that are mundane, dangerous, or impossible for humans to complete, through machine learning.  AI is especially suitable for analyzing massive sets of data to determine patterns, predictions, and other insights that would be impossible for humans.  Individual corporations, as well as entire industries, meticulously track their consumers every move but have been slow to adopt AI and its related benefits.  The hotel industry is an example of an industry that could benefit significantly by analyzing the data they already possess on their customers. 
 
The hotel industry takes a hit to the bottom line each year as the rate of room reservation cancellations continues to rise.  Not only is there a loss of revenue if the room is unable to be rented, but also there are additional expenses related to marketing the room for sale at the last minute [^1].  At the directive of business and marketing experts, hotels have been trying to solve the problem through an increased focus on reservation retention, flexible booking policies, and targeted marketing.  However, even with these efforts, the cancellation rate remains unchecked reaching upwards of 40% in 2019.  By analyzing the data the industry retains on its customers, it would be possible to form a predictive model capable of predicting when a specific customer is likely to cancel a reservation.  A large dataset was sourced that tracked anonymized reservation information for a chain of hotels over a three year period.  Machine learning techniques will be applied to the dataset to form a model capable of producing the aforementioned predictions.  If the model evaluation proves to be statistically significant recommendations will be made to the hotel industry as to how the results should be interpreted as well as actions that may result.

## 2. Background Research and Previous Work

Room reservation completion rates are an important consideration for revenue management in the hotel industry.  Unsurprisingly, there have been previous attempts at creating an algorithm capable of predicting room cancellation rates.  However, these attempts seem to have taken a more general approach such as predicting cancellations by particular ranges of dates [^2].  Other attempts make broad claims about the accuracy of the resulting algorithm without reliably proving so through statistical analysis [^3].  Most importantly for the scope of this course, these previous attempts use subsets of the full dataset available.  This has the potential to lead to unpredictability in the performance of the algorithm.

To differentiate from and improve on the attempts previously mentioned, the algorithm produced as a result of the current effort will not predict the cancellation rate over general stipulations, but rather for a specific customer.  Additionally, a special focus will be on proving that the created algorithm is statistically significant and can accurately be extrapolated to larger subsets of the data.  Finally, for initial training and testing, larger subsets of the datasets will be utilized due to the increased processing power available from Google Colab.  It is important to note that the first-mentioned previous work [^2] appears to use a dataset proprietary to the study while the second-mentioned work [^3] appears to utilize the same dataset that this study will as well.  

## 3. DataSets
Locating a dataset appropriate for this task proved to be challenging.  Privacy concerns and the desire to keep internal corporate information confidential adds difficulty in locating the necessary data.  Ultimately, the following data repository was selected to train and test the reservation cancellation, prediction model:

1. [Hotel Booking Demand](https://www.kaggle.com/jessemostipak/hotel-booking-demand) [^4]

The Hotel Booking Demand dataset contains approximately 120,000 unique entries with 32 describing attributes.  This data comes from a popular data science website, and previous analysis has occurred.  This dataset was featured as part of a small contest on the hosting website where the goal was to predict the likelihood of a guest making a reservation based on certain attributes while this study will instead attempt to predict the likelihood that a reservation is canceled.  The 32 individual attributes of the data will be evaluated for their weight on the outcome of cancellation.  Unlike previously mentioned studies, the attribute describing how the booking was made (in person, online) will be utilized.  Researchers believe that the increase in reservations booked through online third-party platforms is contributing to the increase in cancellation [^5].  Considering this attribute may have a significant impact on the overall accuracy of the developed predictive algorithm.  Finally, the dataset provides information on reservations over the span of a three year period.  During the training and testing phase, an appropriate amount of data will be used from each year to account for trends in cancellations that may have occurred over time.  

|            Attribute           |                          Description                          |
|:------------------------------:|:-------------------------------------------------------------:|
|              hotel             |                  hotel type (resort or city)                  |
|           is_canceled          |              reservation canceled (1) or not (0)              |
|            lead_time           |             # of days between booking and arrival             |
|        arrival_date_year       |                      year of arrival date                     |
|       arrival_date_month       |                     month of arrival date                     |
|    arrival_date_week_number    |              week number of year for arrival date             |
|    arrival_date_day_of_month   |                      day of arrival date                      |
|     stays_in_weekend_nights    |        number of weekend nights (Sat. and Sun.) booked        |
|      stays_in_week_nights      |          number of week nights (Mon. to Fri.) booked          |
|             adults             |                        number of adults                       |
|            children            |                       number of children                      |
|             babies             |                        number of babies                       |
|              meal              |                   meal booked (bb, hb, null)                  |
|             country            |                       country of origin                       |
|         market_segment         |          market segment (online TA, offline, direct)          |
|      distribution_channel      |   booking distribution channel (travel agent, tour operator)  |
|        is_repeated_guest       |                 is repeat guest (1) or not (0)                |
|     previous_cancellations     |        how many times customer has canceled previously        |
| previous_bookings_not_canceled |      how many times customer has completed a reservation      |
|       reserved_room_type       |                       reserved room type                      |
|       assigned_room_type       |                       assigned room type                      |
|         booking_changes        | number of changes made to reservation from booking to arrival |
|          deposit_type          |                  deposit made (1) or not (0)                  |
|              agent             |                     ID of the travel agent                    |
|             company            |                       ID of the company                       |
|      days_in_waiting_list      |       how many days customer took to confirm reservation      |
|          customer_type         |        type of customer (transient, contract, business)       |
|               adr              |                       average daily rate                      |
|   required_car_parking_space   |       number of parking spaces required for reservation       |
|    total_of_special_requests   |                number of special requests made                |
|       reservation_status       |                     status of reservation                     |
|     reservation_status_date    |                  date status was last updated                 |


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
## 5. Progress This Week  
* Updated Abstract
* Updated Title
* Updated Keywords
* Updated Introduction
* Updated Background Research and Previous Work
* Updated DataSets
* Updated README.yaml










## 6. References
[^1]: "Predicting Hotel Booking Cancellations Using Machine Learning - Step by Step Guide with Real Data and Python", Linkedin.com, 2020. [Online]. Available: https://www.linkedin.com/pulse/u-hotel-booking-cancellations-using-machine-learning-manuel-banza/. [Accessed: 08- Nov- 2020].
[^2]: "(PDF) Predicting Hotel Booking Cancellation to Decrease Uncertainty and Increase Revenue", ResearchGate, 2020. [Online]. Available: https://www.researchgate.net/publication/310504011_Predicting_Hotel_Booking_Cancellation_to_Decrease_Uncertainty_and_Increase_Revenue. [Accessed: 08- Nov- 2020].
[^3]: "Predicting Hotel Cancellations with Machine Learning", Medium, 2020. [Online]. Available: https://towardsdatascience.com/predicting-hotel-cancellations-with-machine-learning-fa669f93e794. [Accessed: 08- Nov- 2020].
[^4]: "Hotel booking demand", Kaggle.com, 2020. [Online]. Available: https://www.kaggle.com/jessemostipak/hotel-booking-demand. [Accessed: 08- Nov- 2020].
[^5]: "Global Cancellation Rate of Hotel Reservations Reaches 40% on Average", Hospitality Technology, 2020. [Online]. Available: https://hospitalitytech.com/global-cancellation-rate-hotel-reservations-reaches-40-average. [Accessed: 08- Nov- 2020].