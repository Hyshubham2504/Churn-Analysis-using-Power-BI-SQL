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

---

## Overview
This project demonstrates a comprehensive **end-to-end Churn Analysis** and **Prediction** process using Power BI for visualization, SQL for data manipulation, and Python for machine learning. The goal is to analyze customer churn behavior, identify patterns, and build a predictive model to forecast future churners. 

This project is suitable for telecom firms and adaptable for any industry dealing with customer retention challenges.

---

## Project Goals
- **Analyze customer churn patterns** using data on demographics, geography, services, and account details.
- **Predict future churners** using a Random Forest model, allowing the business to proactively retain customers.
- **Create interactive Power BI dashboards** that provide actionable insights and facilitate decision-making.

---

## Data
The dataset includes customer demographic information, services used, payment details, and churn status. Data was extracted, transformed, and loaded (ETL) using SQL Server and Power Query in Power BI before applying machine learning models.

---

## Process and Methodology

### ETL Process in SQL

1. **Data Loading**:
   Imported the customer data from a CSV file into **SQL Server** using the import wizard, with transformations applied as needed for data consistency.
   ```sql
   CREATE DATABASE db_Churn;
