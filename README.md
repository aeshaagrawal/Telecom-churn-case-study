# Telecom Churn Case Study

## Problem Statement

## Business Problem Overview

In the telecom industry, customers are able to choose from multiple service providers and actively switch from one operator to another. In this highly competitive market, the telecommunications industry experiences an average of 15-25% annual churn rate. Given the fact that it costs 5-10 times more to acquire a new customer than to retain an existing one, customer retention has now become even more important than customer acquisition.

For many incumbent operators, retaining high profitable customers is the number one business goal.

To reduce customer churn, telecom companies need to predict which customers are at high risk of churn.

In this project, we will analyse customer-level data of a leading telecom firm, build predictive models to identify customers at high risk of churn and identify the main indicators of churn.

## Understanding and Defining Churn

There are two main models of payment in the telecom industry - postpaid (customers pay a monthly/annual bill after using the services) and prepaid (customers pay/recharge with a certain amount in advance and then use the services).

In the postpaid model, when customers want to switch to another operator, they usually inform the existing operator to terminate the services, and we directly know that this is an instance of churn.

However, in the prepaid model, customers who want to switch to another network can simply stop using the services without any notice, and it is hard to know whether someone has actually churned or is simply not using the services temporarily (e.g. someone may be on a trip abroad for a month or two and then intend to resume using the services again).

Thus, churn prediction is usually more critical (and non-trivial) for prepaid customers, and the term ‘churn’ should be defined carefully.  Also, prepaid is the most common model in India and southeast Asia, while postpaid is more common in Europe in North America.

This project is based on the Indian and Southeast Asian market.

## Definitions of Churn 

There are various ways to define churn, such as:

**Revenue-based churn:** Customers who have not utilised any revenue-generating facilities such as mobile internet, outgoing calls, SMS etc. over a given period of time. 
There are customers who only receive calls/SMSes from their wage-earning counterparts, i.e. they don’t generate revenue but use the services.

**Usage-based churn:** Customers who have not done any usage, either incoming or outgoing - in terms of calls, internet etc. over a period of time.
The customer who has stopped using the services for a while hence, it may be too late to take any corrective actions to retain them. 

In this project, we will define churn based on customers' usage patterns, specifically identifying those who have not used any revenue-generating services over a specified period. This approach helps identify customers who have stopped using the services, allowing for proactive measures to retain them.

## High-value Churn

In the context of the Indian and Southeast Asian markets, the majority of revenue, around 80%, is generated by the top 20% of customers, known as high-value customers. This highlights the importance of reducing churn among this segment to minimize revenue loss.

In this project, we will identify high-value customers based on a specific metric and concentrate on predicting churn exclusively for this valuable segment.

## Understanding the Business Objective and the Data

The dataset comprises customer-level information for four consecutive months: June (6), July (7), August (8), and September (9). 
The business objective is to predict churn in September (the ninth month) using data from the preceding three months. Gaining insight into typical customer behavior during churn is critical for this predictive analysis.

## Understanding Customer Behaviour During Churn

Customers usually do not decide to switch to another competitor instantly, but rather over a period of time (this is especially applicable to high-value customers). In churn prediction, we assume that there are three phases of customer lifecycle :

1. **The ‘good’ phase:** In this phase, the customer is happy with the service and behaves as usual.

2. **The ‘action’ phase:** The customer experience starts to sore in this phase, for e.g. he/she gets a compelling offer from a  competitor, faces unjust charges, becomes unhappy with service quality etc. In this phase, the customer usually shows different behaviour than the ‘good’ months. Also, it is crucial to identify high-churn-risk customers in this phase, since some corrective actions can be taken at this point (such as matching the competitor’s offer/improving the service quality etc.)

3. **The ‘churn’ phase:** In this phase, the customer is said to have churned. We define churn based on this phase. Also, it is important to note that at the time of prediction (i.e. the action months), this data is not available to us for prediction. Thus, after tagging churn as 1/0 based on this phase, we discard all data corresponding to this phase.

In this scenario, we categorize the four-month period into distinct phases: the first two months are considered the 'good' phase, the third month is the 'action' phase, and the fourth month is the 'churn' phase.


## For a domain-oriented case study in the telecom industry, here's a basic outline:

1. **Introduction**
Overview of the telecom industry and the importance of customer retention.
Objective of the case study: To predict customer churn using machine learning.

2. **Data Description and Data Preprocessing**
Description of the dataset: Features, target variable (churn), and other relevant information.
   a. Derive new features - This is one of the most important parts of data preparation since good features are often the differentiators between good and bad models. We will use our business understanding 
      to derive features that we think could be important indicators of churn.
   b. Filter high-value customers - As mentioned above, we need to predict churn only for the high-value customers. Define high-value customers as follows: Those who have recharged with an amount more than 
      or equal to X, where X is the 70th percentile of the average recharge amount in the first two months (the good phase).
   c. Tag churners and remove attributes of the churn phase - Now tag the churned customers (churn=1, else 0) based on the fourth month as follows: Those who have not made any calls (either incoming or 
      outgoing) AND have not used mobile internet even once in the churn phase. The attributes we need to use to tag churners are: total_ic_mou_9, total_og_mou_9, vol_2g_mb_9, vol_3g_mb_9. After tagging 
      churners, remove all the attributes corresponding to the churn phase.
Explanation of key features such as customer demographics, usage patterns, and service-related information.
Handling missing values.
Encoding categorical variables.
Feature scaling.

4. **Exploratory Data Analysis (EDA)**
Distribution of the target variable (churn).
Analysis of key features and their relationship with churn.
Visualizations to gain insights into the data.

5. **Feature Engineering**
Creation of new features based on domain knowledge.
Selection of relevant features for modeling.

6. **Model Building**
Splitting the data into training and testing sets.
Selection of appropriate machine learning models (e.g., logistic regression, random forest, gradient boosting).
Training the models on the training set.
Build models to predict churn among high-value customers. The predictive model will serve two purposes:
  a. Predict whether a high-value customer will churn in the near future (churn phase), enabling the company to take proactive actions such as offering special plans or discounts on recharge to retain customers.
  b. Identify important variables that strongly predict churn, providing insights into why customers switch to other networks.
In some cases, both of the above-stated goals can be achieved by a single machine learning model. But here, we have a large number of attributes, and thus we should try using a dimensionality reduction technique such as PCA and then build a predictive model. After PCA, we can use any classification model.
Also, since the rate of churn is typically low (about 5-10%, this is called class-imbalance) - we will try using techniques to handle class imbalance. 

8. **Model Evaluation**
Evaluating the models using metrics such as accuracy, precision, recall, and F1-score.
Comparing the performance of different models.

10. **Hyperparameter Tuning**
Fine-tuning the hyperparameters of the models to improve performance.
Finally, choose a model based on some evaluation metric.

12. **Model Interpretation**
Interpreting the results of the models to understand the factors influencing churn.
Identifying key features that contribute to churn prediction (handle class imbalance using appropriate techniques).

13. **Conclusion**
Summary of findings.
Recommendations for the telecom company to reduce customer churn.
Future work and potential improvements to the model.
