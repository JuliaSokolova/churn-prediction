# Customer churn prediction for a ride-sharing company

A ride-sharing company (Company X) is interested in predicting rider retention.

<p align="center"><img width=60% src=https://www.verisk.com/contentassets/590951adf3f04716a6b91ac17a5f528c/white-paper-ridesharing.jpg> 

## Table of Content

- [Objective](#objective)
- [Approach](#approach)
- [Modeling the data](#Modeling the data)
- [Increasing retention](#Increasing retention)
- [What affects the churn](#What affects the churn)
- [Conclusion](#conclusion)


<br>

## Objective 

The goals of our research are:
- Find out what factors are the best predictors for retention
- Propose activities to help Company X improve their business results.

<br>

## Approach

- Use data gathered from Company X
- Clean data with Pandas
- Test different models to predict customers who might churn (Logistic Regression, Random Forest, Gradient Boosting Classifier)
- Tune best performing model (Gradient Boosting Classifier)
- Highlight factors affecting churn
- Propose business activities to increase customer retention

<br>

## Modeling the data

Our raw data included the following elements:

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 50000 entries, 0 to 49999
Data columns (total 14 columns):
 #   Column                  Non-Null Count  Dtype  
---  ------                  --------------  -----  
 0   avg_dist                50000 non-null  float64
 1   avg_rating_by_driver    49799 non-null  float64
 2   avg_rating_of_driver    41878 non-null  float64
 3   avg_surge               50000 non-null  float64
 4   city                    50000 non-null  object 
 5   last_trip_date          50000 non-null  object 
 6   phone                   49604 non-null  object 
 7   signup_date             50000 non-null  object 
 8   surge_pct               50000 non-null  float64
 9   trips_in_first_30_days  50000 non-null  int64  
 10  luxury_car_user         50000 non-null  int64  
 11  weekday_pct             50000 non-null  float64
 12  last_trip               50000 non-null  object 
 13  churn                   50000 non-null  int64  
dtypes: float64(6), int64(3), object(5)
memory usage: 5.3+ MB

```

We did some cleanup (replaced categorical values with dummies, removed NAs, changed date formatting.
With cleaned data, we tested 3 different models - Logistic Regression, Random Forest, Gradient Boosting Classifier.
The difference in accuracy was substantional:
- Logistic Regression: 0.628
- Random Forest: 0.704
- Gradient Boosting Classifier: 0.783

We chose Gradient Boosting Classifier as our go-to model and tuned its parameters.
With learning rate = 0.25 and N_estimators = 550 we got accuracy 0.789.

Our confusion matrix has a precision rate of 0.192. 


<br>

## Increasing retention

To increase customer retention, we propose a campaign, where all users with indication of protential churn get a promotion.
To make sure we give higher promotion to our high-value customers, we came up with an algorithm:

```
monthly_profit_from_user = avg_trips_per_month * surge_pct * 0.75
promotion = monthly_profit_from_user / 2

```

We then run a simulation to calculate our average loss and gain from the promotion.
Here is how our business model looks like:

- monthly revenue for all customers = $ 83,566.05
- potential lost from churn  = -34,275.69

Sending a promotion to our potential churn users, offering them half of our monthly average profit for each user:
- revenue saved  =  17,137.84 
- cost of promotion sent to non-churners = -6,591.96

Total difference: + 10, 546


<br>

## What affects the churn


Factors affecting the churn rate with strongest correlation:
- Average surge
- Using luxury cars


## Conclusion

Moving on, we would suggest runnign our model monthly, while simultaniously training it further.
We also suggest to look out for customers who chose luxury cars / more expensive rides.


