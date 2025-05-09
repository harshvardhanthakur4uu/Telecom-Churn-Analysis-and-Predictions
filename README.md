# Telecom-Churn-Analysis-and-Predictions

## Introduction to Churn Analysis

In today’s competitive business environment, retaining customers is crucial for long-term success. Churn analysis is a key technique used to understand and reduce this customer attrition. It involves examining customer data to identify patterns and reasons behind customer departures. By using advanced data analytics and machine learning, businesses can predict which customers are at risk of leaving and understand the factors driving their decisions. This knowledge allows companies to take proactive steps to improve customer satisfaction and loyalty.

## Project Target
Create an entire ETL process in a database & a Power BI dashboard to utilize the Customer Data and achieve below goals:
1. Visualize & Analyse Customer Data
2. Demographic
3. Geographic
4. Payment & Account Info
5. Services
6. Study Churner Profile & Identify Areas for Implementing Marketing Campaigns
7. Identify a Method to Predict Future Churners Using Machine Learning


## Metrics & KPI's Required
1. Total Customers
2. Total Churn
3. Churn Rate
4. New Joiners

## STEP 1 – ETL Process in SQL Server
So the first step in churn analysis is to load the data from our source file. For this purpose we will be using Microsoft SQL server because it is a widely used solution across the industry and also because a full-fledged Database System is better at handling recurring data loads and maintaining data integrity compared to an excel file.

## STEP 2 – Power BI Transform

Add a new column in prod_Churn

1.       Churn Status = if [Customer_Status] = “Churned” then 1 else 0

2.       Change Churn Status data type to numbers

3.       Monthly Charge Range = if [Monthly_Charge] < 20 then “< 20” else if [Monthly_Charge] < 50 then “20-50” else if [Monthly_Charge] < 100 then “50-100” else “> 100”

 

Create a New Table Reference for mapping_AgeGrp

1.       Keep only Age column and remove duplicates

2.       Age Group = if [Age] < 20 then “< 20” else if [Age] < 36 then “20 – 35” else if [Age] < 51 then “36 – 50” else “> 50”

3.       AgeGrpSorting = if [Age Group] = “< 20” then 1 else if [Age Group] = “20 – 35” then 2 else if [Age Group] = “36 – 50” then 3 else 4

4.       Change data type of AgeGrpSorting to Numbers

 

Create a new table reference for mapping_TenureGrp

1.       Keep only Tenure_in_Months and remove duplicates

2.       Tenure Group = if [Tenure_in_Months] < 6 then “< 6 Months” else if [Tenure_in_Months] < 12 then “6-12 Months” else if [Tenure_in_Months] < 18 then “12-18 Months” else if [Tenure_in_Months] < 24 then “18-24 Months” else “>= 24 Months”

3.       TenureGrpSorting = if [Tenure_in_Months] = “< 6 Months” then 1 else if [Tenure_in_Months] =  “6-12 Months” then 2 else if [Tenure_in_Months] = “12-18 Months” then 3 else if [Tenure_in_Months] = “18-24 Months ” then 4 else 5

4.       Change data type of TenureGrpSorting  to Numbers

 

Create a new table reference for prod_Services

1.       Unpivot services columns

2.       Rename Column – Attribute >> Services & Value >> Status

## STEP 3 – Power BI Measure

        Total Customers = Count(prod_Churn[Customer_ID])

        New Joiners = CALCULATE(COUNT(prod_Churn[Customer_ID]), prod_Churn[Customer_Status] = “Joined”)

        Total Churn = SUM(prod_Churn[Churn Status])

        Churn Rate = [Total Churn] / [Total Customers]

 ## STEP 4 – Power BI Visualization
Summary Page
1.  Top Card <br>
  a. Total Customers <br>
  b. New JoinersTotal <br>
  c. ChurnChurn <br>
  d. Rate% <br>

3.  Demographic<br>
  a. Gender – Churn Rate<br>
  b. Age Group – Total Customer & Churn Rate<br>

4.  Account Info<br>
  a. Payment Method – Churn Rate<br>
  b. Contract – Churn Rate<br>
  c. Tenure Group – Total Customer & Churn Rate<br>

5.  Geographic<br>
  a. Top 5 State – Churn Rate<br>

6.  Churn Distribution<br>
  a. Churn Category – Total Churn<br>
  b. Tooltip : Churn Reason – Total Churn<br>

7.  Service Used<br>
  a. Internet Type – Churn Rate<br>
  b. prod_Service >> Services – Status – % RT Sum of Churn Status<br>

Churn Reason Page (Tooltip)
1.  Churn Reason – Total Churn

STEP 5 – Predict Customer Churn

For predicting customer churn, widely used Machine Learning algorithm called RANDOM FOREST is used for our model.

What is Random Forest?A random forest is a machine learning algorithm that consists of multiple decision trees. Each decision tree is trained on a random subset of the data and features. The final prediction is made by averaging the predictions (in regression tasks) or taking the majority vote (in classification tasks) from all the trees in the forest. This ensemble approach improves the accuracy and robustness of the model by reducing the risk of overfitting compared to using a single decision tree.

## STEP 6 – Power BI Visualization of Predicted Data

Import CSV Data or Load Predicted data in SQL server & connect to server

 
Create Measures

    Count Predicted Churner = COUNT(Predictions[Customer_ID]) + 0
    Title Predicted Churners = “COUNT OF PREDICTED CHURNERS : ” & COUNT(Predictions[Customer_ID])

 

Churn Prediction Page (Using New Predicted Data)
1.  Right Side Grid<br>
  a. Customer ID<br>
  b. Monthly Charge<br>
  c. Total Revenue<br>
  d. Total Refunds<br>
  e. Number of Referrals<br>

2.  Demographic<br>
  a. Gender – Churn Count<br>
  b. Age Group – Churn Count<br>
  c. Marital Status – Churn Count<br>

3.  Account Info<br>
  a. Payment Method – Churn Count<br>
  b. Contract – Churn Count<br>
  c. Tenure Group – Churn Count<br>

4.  Geographic<br>
  a. State – Churn Count<br>
