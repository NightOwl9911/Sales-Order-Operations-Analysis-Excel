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
![Top 10 Products with Missing CustomerID](/images/Report%201/Top%2010.png)

![Total Transactions Analysis](/images/Report%201/Total%20Transactions%20Analysis.png)

Approximately 24.9% of all transaction records are missing CustomerID information, which significantly limits customer-level reporting and operational visibility. The issue does not appear to be randomly distributed, as several products such as DOTCOM POSTAGE and multiple JUMBO BAG variants account for a disproportionately large share of these transactions. Further investigation should determine whether the missing CustomerIDs originate from a specific sales channel, order process, or data capture issue.

-	Is 24.93% actually bad?

I would consider it a potential concern because nearly one-quarter of transactions cannot be linked to a customer. However, before concluding that it is a problem, I would investigate whether these transactions are expected to be anonymous, system-generated, or tied to a specific business process.



### 2. ❌ Report 2 - Order Cancellation Analysis
![Cancellation Analysis](/images/Report%202/Cancellation%20Analysis.png)
A total of 3,836 orders were cancelled out of 25,900 orders, resulting in an overall cancellation rate of 14.81%. This indicates that approximately one out of every seven orders was cancelled, highlighting a potential opportunity to improve operational efficiency and reduce revenue loss.

![Top 15 Highest Cancellation Rate Products](/images/Report%202/Top%2015%20Highest%20Cancellation%20Rate%20Products.png)

The analysis identified several products with cancellation rates significantly above the overall average. After excluding non-sellable records such as Discount, Amazon Fee, Bank Charges, and Manual, the products with the highest cancellation rates were Cinderella Chandelier (29.41%), Set Of 3 Babushka Stacking Tins (28.57%), and Vintage Blue Kitchen Cabinet (22.22%). These products should be prioritized for further investigation to determine whether inventory constraints, pricing issues, fulfillment challenges, or customer purchasing behavior are contributing to the elevated cancellation rates.

![Countries with the Highest Cancellation Rate](/images/Report%202/Cancellation%20Rate%20by%20Country.png)

Although the United Kingdom generated the highest number of cancelled orders, its cancellation rate (14.35%) remained close to the overall average due to its significantly higher order volume. Countries such as Japan (32.14%), Italy (30.91%), Switzerland (27.03%), and Germany (24.21%) exhibited substantially higher cancellation rates, suggesting potential operational or market-specific challenges that warrant further investigation.

![Cancellation Trend](/images/Report%202/Cancellation%20Trend.png)

Monthly trend analysis revealed that cancellations remained relatively stable throughout most of the period before increasing during the final quarter of 2011, reaching their highest level in November 2011. This pattern may indicate seasonal demand effects, inventory constraints, or operational challenges during peak periods and should be investigated further to identify the underlying causes.



### 3. 👥 Report 3 - Customer Analysis

![Top 10 Customers By Revenue](/images/Report%203/Customer%20by%20Revenue.png)

The analysis identified the customers generating the highest revenue for the company. While these customers do not necessarily place the highest number of orders, they contribute significantly to overall business performance and revenue generation. Understanding their purchasing behavior and product preferences can help support revenue growth, customer retention, and strategic account management.

**Key Finding:** Customer 14646 generated the highest revenue, contributing approximately $279,489.


![Top 10 Customer By Sales Volume](/images/Report%203/Customer%20by%20Sales%20Volume.png)

The analysis identified the customers placing the highest number of orders. These customers represent a substantial share of operational activity and may require greater attention from customer service, order management, and fulfillment teams. Monitoring their ordering patterns can help improve demand planning and operational efficiency.

**Key Finding:** Customer 14911 placed the highest number of orders, with 248 transactions.

![Top 20 Customers by Cancellation Rate](/images/Report%203/Top%2020%20Customers%20by%20Cancellation%20Rate.png)

The analysis revealed a group of customers with exceptionally high cancellation rates, several exceeding 50% of their total orders. Frequent cancellations may indicate issues related to product availability, pricing, delivery expectations, order accuracy, or customer-specific purchasing behavior. These customers should be prioritized for further investigation to identify and address the underlying causes.

**Key Finding:** Customer 13115 exhibited the highest cancellation rate at 71.43%, with 10 cancelled orders out of 14 total orders.



### 4. 📦 Report 4 - Product Analysis

![Top 20 Products by Sales Volume](/images/Report%204/Products%20by%20Sales%20Volume.png)

The analysis identified the products generating the highest sales volume based on completed orders. These products represent the largest share of operational activity and therefore have the greatest impact on inventory management, warehouse operations, picking, packing, and fulfillment processes. Monitoring high-volume products is essential to ensure inventory availability and maintain operational efficiency.

**Key Finding:** **Paper Craft**, **Little Birdie** and **Medium Ceramic Top Storage Jar** recorded the highest sales volumes, generating significant demand and operational workload across the fulfillment process.

![Top 20 Products by Revenue](/images/Report%204/Products%20by%20Revenue.png)

The analysis identified the products contributing the most revenue to the business. While some overlap exists between high-volume and high-revenue products, the results confirm that products with the highest sales quantities do not necessarily generate the highest revenue. Understanding these products is critical for revenue protection and commercial performance.

**Key Finding:** **Dotcom Postage**, **Regency Cakestand 3 Tier**, and **Paper Craft, Little Birdie** generated the highest revenue contributions, making them strategically important products for overall business performance.

![Top 20 Highest Cancellation Rate Products with Revenue](/images/Report%204/Top%2020%20Highest%20Cancellation%20Rate%20Products%20with%20Revenue.png)

The analysis identified products with the highest cancellation rates after excluding non-sellable records such as Discount, Samples, Amazon Fee, Bank Charges, and Manual. Several products exhibited cancellation rates significantly above the overall average, indicating potential operational and commercial risks. Elevated cancellation rates may be associated with inventory constraints, pricing issues, fulfillment challenges, product-specific demand patterns, or customer expectations.

**Key Finding:** **Cinderella Chandelier** exhibited the highest cancellation rate among sellable products at 30.30%, followed by **Vintage Blue Kitchen Cabinet** (23.08%) and **Rococo Wall Mirror White** (20.69%).

#### Business Impact

Analyzing products from multiple perspectives—including sales volume, revenue contribution, and cancellation behavior—provides a more comprehensive understanding of product performance. This approach helps identify operational bottlenecks, prioritize inventory and fulfillment improvements, protect revenue-generating products, and reduce avoidable cancellations. Combining these metrics enables organizations to focus improvement efforts where they can create the greatest operational and financial impact.

## 📝 Executive Summary & Recommendations

The analysis identified three primary operational risk areas: incomplete customer information, elevated order cancellation rates, and specific products and customers exhibiting abnormal cancellation behavior.

Approximately 24.93% of transactions contained missing Customer IDs, limiting customer-level visibility and reducing the effectiveness of customer analytics. Additionally, 14.81% of all orders were cancelled, with certain products and countries exhibiting cancellation rates significantly above the overall average.

The customer analysis revealed that high-revenue customers are not necessarily the same customers generating the highest transaction volume, highlighting the importance of evaluating customer value from multiple perspectives. Product analysis further demonstrated that high-volume products, high-revenue products, and high-cancellation products represent distinct operational categories that should be monitored independently.

Based on these findings, the organization should prioritize improving customer data quality, investigating the root causes of order cancellations, and implementing monitoring frameworks for high-value customers and products. These actions can improve operational efficiency, forecasting accuracy, customer satisfaction, and revenue protection.

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