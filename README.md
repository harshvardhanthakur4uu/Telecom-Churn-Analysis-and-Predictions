# Telecom-Churn-Analysis-and-Predictions

## Introduction to Churn Analysis

In today’s competitive business environment, retaining customers is crucial for long-term success. Churn analysis is a key technique used to understand and reduce this customer attrition. It involves examining customer data to identify patterns and reasons behind customer departures. By using advanced data analytics and machine learning, businesses can predict which customers are at risk of leaving and understand the factors driving their decisions. This knowledge allows companies to take proactive steps to improve customer satisfaction and loyalty.

## Project Target
Create an entire ETL process in a database & a Power BI dashboard to utilize the Customer Data and achieve below goals:
1. Visualize & Analyse Customer Data at below levels
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
