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

#### 1. 🛠️ General Data Cleaning 

- **Removed Duplicates:** Based on the information available in the dataset, duplicate records were removed only when the following columns contained identical values: InvoiceNo, Quantity, InvoiceDate, and CustomerID.

- **Standardized Data Types:** Several fields were converted to the appropriate data types to ensure consistency and accuracy throughout the analysis. The following transformations were applied in Power Query:

InvoiceDate: Text → Date

InvoiceNo: Any → Text

CustomerID: Any → Text

- **Added Analytical Columns:** To support deeper analysis and reporting, three additional columns were created using the existing dataset information:

    - **Cancelled Product?** – Identifies whether a transaction was cancelled or successfully processed by evaluating the invoice number pattern.
    - **Sales** – Calculates the total sales value for each transaction by multiplying Unit Price by Quantity.
    - **IDCustomer?** – Indicates whether a transaction is associated with a valid customer ID or contains a blank/null value, allowing for the analysis of identified versus unidentified customers.

- **Standardized Product Descriptions:** During data validation, it was identified that some Stock Codes were associated with multiple product descriptions. To ensure consistency, descriptions were standardized by assigning the most frequently occurring description to each Stock Code. This approach helped maintain a single, consistent product description across the dataset while preserving the most representative value.


**Clean Dataset**: After completing the general data cleaning process, the resulting dataset (Online Retail Clean) became the primary source for all subsequent analyses. The following reports and their associated queries were built using this cleaned dataset.

#### 2. ⚠️ Report 1 - Missing Customer Information
For this report, the Online Retail Clean dataset was used as the source query. The following transformations were performed:

- Selected the IDCustomer? column previously created to distinguish transactions with and without a valid CustomerID.
- Grouped the records to calculate the total number of transactions for each category.
Pivoted the resulting values to convert the grouped categories from rows into columns for easier analysis.
- Added a Total Transactions column to calculate the overall number of transactions.
- Added a Missing Customer ID % column to calculate the percentage of transactions without an associated CustomerID.

These steps enabled the identification and quantification of transactions lacking customer information, providing insight into the completeness and quality of the customer data.

Query Names Used -> **Online Retail Clean** and **Transactions Query**


#### 3. ❌ Report 2 - Order Cancellation Analysis

For this report, the Online Retail Clean dataset was used as the source query. The following transformations were performed:

- Retained only the relevant columns: InvoiceNo, StockCode, Description, Country, and Cancelled Product?.
- Created a new column named Product Cancelled based on the values in the Cancelled Product? column.
- Converted the original binary values (1 = Yes, 0 = No) into more user-friendly labels (Yes and No) to improve readability and facilitate analysis.
- Removed the Cancelled Product? column after creating the new descriptive field, as it was no longer required.

These transformations simplified the dataset and provided a clearer view of cancelled versus completed transactions, enabling a more intuitive cancellation analysis.

Query Names Used -> **Cancellation Analysis** and **Cancellation Trend by Country**

#### 4. 👥 Report 3 - Customer Analysis

For this report, the Online Retail Clean dataset was used as the source query. The following transformations were performed:

- Retained only the relevant columns: InvoiceNo, Cancelled Product?, Sales, and CustomerID.
- Removed records with blank or null values in the CustomerID column to focus the analysis on identified customers.
- Created a new descriptive field by converting the binary values in Cancelled Product? (1 = Yes, 0 = No) into more user-friendly labels (Yes and No) to improve readability and facilitate analysis.
- Removed the original Cancelled Product? column after creating the new descriptive field, as it was no longer required.

These transformations ensured that the dataset contained only valid customer transactions and provided a clearer framework for analyzing customer behavior, purchasing activity, and cancellation patterns.

Query Name Used -> **Customer Order Sales**


#### 5. 📦 Report 4 - Product Analysis

For this report, the Online Retail Clean dataset was used as the source query. The following transformations were performed:

- Filtered the Unit Price column to retain only records with values greater than 0, as it was identified that transactions with a Unit Price of 0 were associated with negative quantities and did not represent valid sales transactions.
- Retained only the relevant columns: InvoiceNo, StockCode, PreferredDescription, Quantity, Cancelled Product?, and Sales.
- Created a new descriptive field by converting the binary values in Cancelled Product? (1 = Yes, 0 = No) into more user-friendly labels (Yes and No) to improve readability and facilitate analysis.
- Removed the original Cancelled Product? column after creating the new descriptive field, as it was no longer required.

These transformations prepared the dataset for product-level analysis by excluding invalid transactions, simplifying cancellation indicators, and retaining only the fields necessary to evaluate product performance, sales trends, and order quantities.

Query Name Used -> **Product Order Sales**

## 📊 Analysis

### 1. ⚠️ Report 1 - Missing Customer Information
![Top 10 Products with Missing CustomerID](/images/Report%201/Top%2010%20Product%20with%20Missing%20CustomerID.png)

![Total Transactions Analysis](/images/Report%201/Total%20Transactions%20Analysis.png)


### 2. ❌ Report 2 - Order Cancellation Analysis
![Top 15 Highest Cancellation Rate Products](/images/Report%202/Top%2015%20Highest%20Cancellation%20Rate%20Products.png)

![Countries with the Highest Cancellation Rate](/images/Report%202/Countries%20with%20the%20Highest%20Cancellation%20Rate.png)

![Cancellation Trend](/images/Report%202/Cancellation%20Trend.png)
![Cancellation Analysis](/images/Report%202/Cancellation%20Analysis.png)


### 3. 👥 Report 3 - Customer Analysis
![Top 10 Customers By Revenue](/images/Report%203/Top%2010%20Customers%20By%20Revenue.png)
![Top 10 Customer By Sales Volume](/images/Report%203/Top%2010%20Customer%20By%20Sales%20Volume.png)
![Top 20 Customers by Cancellation Rate](/images/Report%203/Top%2020%20Customers%20by%20Cancellation%20Rate.png)


### 4. 📦 Report 4 - Product Analysis
![Top 20 Products by Sales Volume](/images/Report%204/Top%2020%20Products%20by%20Sales%20Volumen.png)
![Top 20 Products by Revenue](/images/Report%204/Top%2020%20Products%20by%20Revenue.png)
![Top 20 Highest Cancellation Rate Products with Revenue](/images/Report%204/Top%2020%20Highest%20Cancellation%20Rate%20Products%20with%20Revenue.png)





## 💡 Key Skills Demonstrated
Throughout this project, the following analytical, technical, and business skills were applied:

- Data Cleaning
- Data Validation
- Business Analysis
- Root Cause Analysis
- Operational Reporting
- KPI Development
- Microsoft Excel
- Power Query
- Pivot Tables
- Stakeholder-Oriented Reporting
- Data Transformation
- Data-Driven Decision Making
- Performance Analysis
- Insight Generation and Communication

This project demonstrates the end-to-end process of transforming raw transactional data into actionable business insights through data preparation, analysis, and reporting.

## 🚀 Future Improvements 

This project can be further enhanced by incorporating additional data sources and expanding the scope of the analysis. Potential future improvements include:

- Customer Lifetime Value (CLV) Analysis – Evaluate the long-term value generated by each customer and identify high-value customer segments.
- Revenue Lost Due to Cancellations – Quantify the financial impact of cancelled orders and identify patterns driving revenue loss.
- Product Profitability Analysis – Analyze product-level profitability by incorporating cost and margin data.
- Power BI Dashboard Version – Develop an interactive dashboard to enable dynamic exploration of key metrics and insights.
- SQL Implementation – Recreate the data transformation and reporting process using SQL to demonstrate database querying and data modeling capabilities.
- Geographical Sales Analysis – Explore sales performance across countries and regions to identify market opportunities and trends.
- Customer Retention Analysis – Measure repeat purchase behavior and customer retention rates over time.

These enhancements would provide deeper business insights and further strengthen the analytical value of the project.

## ✅ Personal Takeaway

This analysis reinforced the importance of evaluating products from multiple perspectives rather than relying on a single metric. Product performance should be assessed not only through sales volume and revenue contribution, but also through cancellation behavior and other operational indicators.

For example, a product that generates substantial revenue may initially appear successful; however, if it also exhibits a high cancellation rate, it could represent a significant operational and financial risk. Such patterns may indicate underlying issues related to inventory availability, order fulfillment, product quality, or customer expectations.

By combining these metrics, I can better identify high-impact areas, prioritize investigations, and recommend improvements that deliver meaningful business value. This approach enables more informed decision-making and supports continuous improvement across both operational and commercial processes.