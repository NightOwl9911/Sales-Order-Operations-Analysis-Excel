<h1 align="center">🟩 Sales Order Operations Analysis with Excel and Power Query </h1>


## 📋 Project Overview
This project analyzes sales order transactions using Excel and Power Query to identify operational risks, customer behavior patterns, cancellation drivers, and product performance. The analysis simulates the type of investigations commonly performed by Sales Order Processing Analyst and Operations Analyst to support decision-making and process improvement.

## 🎯 Business Problem
Online-retail organization experienced (data from 2010 - 2011) order cancellations, incomplete customer records, and varying product performance. Management requires visibility into operational risks affecting revenue, customer experience and order fulfillment efficiency. 

## 🥅 Objectives
- Identify customer missing information.
- Analyze order cancellation behavior.
- Identify high-value customers.
- Evaluate product performance.
- Detect operational risks.
- Provide business recommendation.


## 🗄️ Dataset

The dataset in study is provided by UCI (University of California, Irvine) from their Machine Learning Repository.

You can find it here ->
[Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail)

It contains:
- Invoice Numbers and Dates 
- Customer IDs
- Product Information (Description and Stock codes)
- Quantities
- Unit Price
- Country Information
- Cancellation Records

## 🛠️ Tools Used
For the completion of the project, the following tools were implemented:
- Microsoft Excel
- Power Query
- Pivot Tables
- Primary Excel Functions used:

    - XLOOKUP
    - COUNTIFS
    - SUMIFS
    - Conditional Formatting 


## 🧹 Data Cleaning

This project consists in 4 reports. For each one, there was a different data cleaning process implemented but a general one to prepare the data.

1. 🛠️ General Data Cleaning 

- Removed Duplicates: Based on the information available in the dataset, duplicate records were removed only when the following columns contained identical values: InvoiceNo, Quantity, InvoiceDate, and CustomerID.

- Standardized Data Types: Several fields were converted to the appropriate data types to ensure consistency and accuracy throughout the analysis. The following transformations were applied in Power Query:

InvoiceDate: Text → Date

InvoiceNo: Any → Text

CustomerID: Any → Text

- Standardized Product Descriptions: During data validation, it was identified that some Stock Codes were associated with multiple product descriptions. To ensure consistency, descriptions were standardized by assigning the most frequently occurring description to each Stock Code. This approach helped maintain a single, consistent product description across the dataset while preserving the most representative value.

2. ⚠️ Report 1 - Missing Customer Information


3. ❌ Report 2 - Order Cancellation Analysis


4. 👥 Report 3 - Customer Analysis


5. 📦 Report 4 - Product Analysis


## 📊 Analysis

### 1. ⚠️ Report 1 - Missing Customer Information
### 2. ❌ Report 2 - Order Cancellation Analysis
### 3. 👥 Report 3 - Customer Analysis
### 4. 📦 Report 4 - Product Analysis

## 💡 Key Skills Demonstrated

## 🚀 Future Improvements 

## ✅ Conclusion