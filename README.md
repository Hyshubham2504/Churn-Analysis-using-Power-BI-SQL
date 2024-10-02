# Churn Analysis and Prediction Using Power BI, SQL, and Machine Learning

## Table of Contents
- [Overview](#overview)
- [Project Goals](#project-goals)
- [Data](#data)
- [Process and Methodology](#process-and-methodology)
  - [ETL Process in SQL](#etl-process-in-sql)
  - [Data Exploration](#data-exploration)
  - [Power Query Transformations](#power-query-transformations)
  - [Machine Learning Model](#machine-learning-model)
- [Power BI Dashboards](#power-bi-dashboards)
  - [Churn Analysis - Summary](#churn-analysis---summary)
  - [Churn Prediction Dashboard](#churn-prediction-dashboard)
- [Key Insights](#key-insights)
- [How to Use](#how-to-use)
- [Technologies Used](#technologies-used)

## Overview
This project demonstrates a comprehensive end-to-end Churn Analysis and Prediction process using Power BI for visualization, SQL for data manipulation, and Python for machine learning. The goal is to analyze customer churn behavior, identify patterns, and build a predictive model to forecast future churners. This project is suitable for telecom firms and adaptable for any industry dealing with customer retention challenges.

## Project Goals
- Analyze customer churn patterns using data on demographics, geography, services, and account details.
- Predict future churners using a Random Forest model, allowing the business to proactively retain customers.
- Create interactive Power BI dashboards that provide actionable insights and facilitate decision-making.

## Data
The dataset includes customer demographic information, services used, payment details, and churn status. Data was extracted, transformed, and loaded (ETL) using SQL Server and Power Query in Power BI before applying machine learning models.

## Process and Methodology

### ETL Process in SQL
1. **Data Loading**: Imported the customer data from a CSV file into SQL Server using the import wizard, with transformations applied as needed for data consistency.
    ```sql
    BULK INSERT Sales_Data
    FROM 'c:\sales_data.csv'
    WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n');
    ``` 

2. **Data Cleaning and Transformation**: Removed null values and handled missing data using SQL's ISNULL function.
    ```sql
    UPDATE Sales_Data
    SET [Customer_ID] = ISNULL([Customer_ID], 0),
        [Title] = ISNULL([Title], 'N/A'),
        [Marital_Status] = ISNULL([Marital_Status], 'N/A')
    WHERE Customer_ID is NULL;
    ```

3. **Views for Power BI**
Created views in SQL Server for easy integration with Power BI dashboards:
    ```sql
    -- Create VIEW: v_ChurnedViews as Customer_Status for easy integration with Power BI dashboards.
    CREATE VIEW v_ChurnedViews AS
    SELECT Customer_ID, ChurnedStatus_in_SQLServer_Terminology AS 'Churned', Stayed AS 'Stay'
    FROM dbo.Customer_Data;
    ```

## Exploration Data Analysis (EDA)
Performed Exploratory Data Analysis (EDA) in SQL by checking for distinct values and nulls across various columns, such as Gender, State, Customer_Status, and Contract.
    ```sql
    -- Perform exploratory statistical analysis by checking for distinct values and nulls.
    SELECT COUNT(DISTINCT Customer_ID) as TotalCustomers,
           COUNT(DISTINCT Gender) as TotalGender,
           COUNT(DISTINCT Marital_Status) as TotalMaritalStatus,
           SUM(CASE WHEN ChurnedStatus_in_SQLServer_Terminology = 1 THEN 1 ELSE 0 END) as ChurnedCustomers,
           SUM(CASE WHEN Stayed = 1 THEN 1 ELSE 0 END) as StayedCustomers
    FROM dbo.Customer_Data;
    ```

## Power Query Transformations
Power Query was used for additional transformations after loading the data from SQL Server into Power BI.

## 1. New COlumn
 Created a new `Churn_Status` column: 1 for churned customers and 0 otherwise.
```powerquery
Churn_Status = if [Customer_Status] = "Churned" then 1 else 0

## 2. Binning
Grouped Monthly_Charges into predefined ranges for better analysis of customer billing behavior.
```powerquery
Monthly_Charge_Range = if [Monthly_Charge] < 20 then "<20" else if [Monthly_Charge] < 60 then "20-59" else "60+"

## 3. Grouping by Age and Tenure
Created age and tenure groups for easier segmentation of customer data.
```powerquery
Age_Group = if [Age] < 20 then "<20" else if [Age] < 36 then "20-35" else if [Age] < 50 then "36-49" else "50+"

## 4. Unpivoting
Unpivoted service-related columns to make the data more accessible for analysis.



