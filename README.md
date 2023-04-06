# NYC Taxi Trip Time Prediction (ML-Regression)

## Project Description

The recent rapid developments in technology have caused the transportation sector to change considerably. The need for transportation has grown significantly as a result of the world's population surpassing 7 billion. The need for mobility has joined the three fundamental needs of food, water, and shelter, which has prompted the development of more effective forms of transit like internet- and app-based systems.

New York City is one of the places that has embraced this technology and made significant advancements in transportation. With a comprehensive network of subways, buses, and taxi services, New York City is one of the most technologically sophisticated cities in the world when it comes to transit. There are more than 10,000 taxis in the metropolis, and more than 100 million taxi journeys take place annually. It's interesting to note that almost 50% of city residents don't own a personal car, which means that many depend heavily on cabs as their main form of transportation.

With the advent of app-based services like Uber and Lyft, the cab business in New York City has experienced major changes in recent years. These services have simplified the processes for booking, tracking, and paying for taxis. The rivalry in the cab industry has grown as a result of the app-based services, leading to better services and reduced costs for consumers.A great illustration of how technology can transform transportation and make it more effective, cheap, and available to everyone is New York City. The introduction of app-based services has made it simpler and more practical for people to get around the city, and the city's taxi business has adjusted to these changes.

## Problem Statement

The problem statement is to develop a prediction algorithm that will help determine and predict the trip duration of taxi. As a result, this would make it easier to quickly and effectively match the right cabs with the right clients.

## Table of Contents
- [Data Summary](#data-summary)
- [Project Code and Approach](#project-code-and-approach)
- [Conclusion](#conclusion)
- [Future Scope](#future-scope)

## Data Summary

The dataset is based on the 2016 NYC Yellow Cab trip record data made available in Big Query on Google Cloud Platform. The contents of NYC Taxi Time Prediction are:

| Column Name         | Description                                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------|
| id                  | A unique identifier for each trip.                                                                 |
| vendor_id           | A code indicating the provider associated with the trip record.                                   |
| pickup_datetime     | Date and time when the meter was engaged.                                                         |
| dropoff_datetime    | Date and time when the meter was disengaged.                                                       |
| passenger_count     | The number of passengers in the vehicle (driver entered value).                                    |
| pickup_longitude   | The longitude where the meter was engaged.                                                         |
| pickup_latitude    | The latitude where the meter was engaged.                                                          |
| dropoff_longitude  | The longitude where the meter was disengaged.                                                       |
| dropoff_latitude   | The latitude where the meter was disengaged.                                                        |
| store_and_fwd_flag  | This flag indicates whether the trip record was held in vehicle memory before sending to the vendor |
| trip_duration       | Duration of the trip in seconds.                                                                   |


## Project Code and Approach

The full code for this article can be found [here](https://github.com/prasantsahoo107/NYC-Taxi-Trip-Time-Prediction-ML-Regression). The code is implemented in Python, and various machine learning algorithms are utilized. Below is a brief description of the general approach employed:

### Data Loading and General Checkups

We have loaded the data from the given CSV files using a function from the Pandas library. Then we checked the general information about the data.

### Exploratory Data Analysis

We removed the ID variable, as it does not provide much interpretation. We then calculated the distance based on the Haversine formula from pickup and drop-off latitude and longitude. Then we plotted a box plot for the distance variable and observed that there are many outliers. So we segregated this variable and found that most of the trips are within 10 km, some trips are within 50 km, while very few trips cross 50 km. Therefore, we eliminated trips with a distance of 0 km and above 50 km. 

We then checked the categorical variables `store_and_fwd_flag` and `passenger_count`. We observed that the `store_and_fwd_flag` variable contains a majority of one category. So we dropped this feature. The `passenger_count` variable has entries from 0 to 9. Since there are no trips with 0 passengers, either this is a misentry or the driver forgot to enter the passenger count of that trip. Also, in a taxi, a maximum of six persons are allowed to sit, including minors. So we eliminated the 0 and 7-9 records from our dataset.

### Linear Regression

Linear regression is a regression of the dependent variable on the independent variable. It is a linear model that assumes a linear relationship between the dependent (y) and independent variables (x).

### XGBoost

XGBoost comes under boosting and is known as extra gradient boosting. GBM first calculates the model using X and Y, then after the prediction is obtained, it will again calculate the model based on the residual of the previous model. Here, the loss function will give more weightage to the error of the previous model.

### LightGBM

Light GBM is based on the decision tree algorithm. But it splits the tree leaf-wise rather than level-wise like other boosting algorithms. So, when growing on the same leaf in Light GBM, the leaf-wise algorithm can reduce more loss than the level-wise algorithm, resulting in much better accuracy, which can rarely be achieved by any of the existing boosting algorithms.

## Conclusion

- The project covered various aspects of the machine learning development cycle.
 - Data exploration and variable analysis are essential parts of the cycle and should be conducted to achieve a comprehensive understanding of the data.
 - The data was cleaned during the exploration phase to handle outliers before feature engineering.
 - Feature engineering was carried out to extract optimal features that are significant and cover most of the variance in the dataset.
 - The models were trained on the optimum featureset to obtain the results.
 - The analysis indicates that the two models have similar learning rates, but with discernible differences in error rates.
 - Gradient boosting exhibits superior performance compared to all other models.
XGBoost's training curve shows a low initial error rate, which improves with an increase in training size and eventually plateaus towards the end.
 - The validation curves of both models follow a similar trend, with high initial error rates that progressively decrease as the training size increases, albeit with varying degrees of accuracy.
 - Both models exhibit high variance, as evidenced by their low training curve errors.
 - The significant gap observed towards the end suggests a low bias, indicating potential overfitting of the training data.
 - Both models have the potential to decrease further and converge towards the training curve by the end.

### Key Findings
- The XGBoost and LightGBM algorithms outperformed the linear regression model.
- Data cleaning was essential in handling outliers before feature engineering.

## Future Scope
To improve the model, we could consider the following steps:
- Add more training instances to improve the validation curve in the XGBoost model.
- Increase the regularization for the learning algorithm, which would decrease the variance and increase the bias towards the validation curve.
- Consider reducing the number of features in the training data that we currently use. This would still allow the algorithm to fit the training data well, but due to the decreased number of features, it would build less complex
