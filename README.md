# Data Analysis and Management Framework for E-commerce

This document provides a comprehensive analysis of sales and customer data, starts with data accuracy check’s, Outline Requirements, Data Modeling Steps. Also Exploring key metrics such as transaction volumes, sales amounts, and purchasing trends across different demographics and regions, while also identifying actionable insights for enhancing customer engagement and driving business growth.

## I. Verify the Accuracy, Completeness, and Reliability of Source Data:
#### * Cross-Referencing: 

Compared the data against known reliable values to validate accuracy and completeness.
Findings are some of the column’s values in Customer table contains Special characters. 

<img width="302" alt="image" src="https://github.com/user-attachments/assets/87e7e4ed-45f6-4606-b3e9-7ad512c13a33">

Fig: 1

**Validation Rules:** Defined specific validation rules based on the requirements (e.g., acceptable value, data type checks).

#### * Data Profiling:

I have used in-build data profiling feature to analyze the source data for anomalies, missing values, 
duplicates, and inconsistencies.

<img width="434" alt="image" src="https://github.com/user-attachments/assets/ea6cf6cd-81a3-42b7-a941-f3553e787152">

Fig:2. Data profiling for Customer table

<img width="434" alt="image" src="https://github.com/user-attachments/assets/ac1fed62-5caa-41da-af07-7ce225830f3e">

Fig:3. Data profiling for Order table 

<img width="434" alt="image" src="https://github.com/user-attachments/assets/3b9363b7-4861-4600-b8e4-f1a324e03087">

Fig:4. Data profiling for Shipping table


#### * Verified Checklist:

**Completeness:** Confirmed that all required fields are populated and check for missing records.

**Consistency:** Validated that data formats are uniform across datasets (e.g., date formats, naming conventions). But some of the column’s values in Customer table contains Special characters.

**Timeliness:** Assess whether the data is up-to-date and relevant for current analysis needs.

## II. Requirements Specification:

#### A.  Data Components:
  - Entities: Defined the main entities (e.g., Customers, Orders, Products).
  - Attributes: Specify necessary attributes for each entity (e.g., Customer ID, Name, Age, Order Amount).
  - Relationships: Outlined relationships between entities (e.g., one-to-many between Customers and Orders).
##### B.  Quality Requirements:
  - Defined acceptable thresholds for data quality metrics (e.g., accuracy > 95%, completeness > 90%).

## III. Developed Data Models:

#### High-Level Data Entities and Their Relationships

#### 1. Entities Overview
###### 1. Customer
Attributes:
Customer_ID (Primary Key),
First_Name,
Last_Name,
Age,
Country

###### 2. Order
 Attributes:
Order_ID (Primary Key),
Customer_ID (Foreign Key),
Amount,
Status

###### 3.Shipping
Attributes:
Shipping_ID (Primary Key),
Customer _ID (Foreign Key),
Status

#### 2. Relationships Between Entities
###### Customer to Order:
Type: One-to-Many
Description: A customer can place multiple orders, but each order is associated with only one customer.
Relation:
Customer_ID in the Order entity references Customer_ID in the Customer entity.

###### Customer to Shipping:
Type: One-to-Many
Description: A customer can have multiple shipping records associated with their orders.
Relation:
Customer_ID in the Shipping entity references Customer_ID in the Customer entity.
###### Order to Shipping:
Type: One-to-One
Description: Each order has a corresponding shipping record, indicating the delivery status and details.
Relation:
Order_ID in the Shipping entity references Order_ID in the Order entity.

**Physical Model:**

<img width="608" alt="Screenshot 2024-09-27 at 6 26 26 PM" src="https://github.com/user-attachments/assets/7c6792fc-c9df-4e73-81ac-e781554f768e">

## IV.  Technical Specifications:

#### 1. Data Sources and Ingestion:
The data pipeline will need to ingest data from the following sources:
###### Customer Data:
Source: CRM Database (e.g, MySQL)( 'Customer.xls')
Key Columns: Customer_ID, First_Name, Last_Name, Country
###### Order Data:
Source: Order Management System(‘'Order.csv')
Key Columns: Order_ID, Customer_ID, Total_Amount, Status
###### Shipping Data:
Source: Shipping/Delivery Management API('Shipping.json')
Key Columns: Shipping_ID, Customer_ID, Status
#### 2. Data Extraction
 we will extract data from the following sources: 
 
**Customer and Order Data:** Perform SQL queries to retrieve all necessary fields. The data should be extracted periodically (daily or as necessary) to capture new or updated records.

**Shipping Data:** Pull real-time shipping updates through API calls to the external shipping system and store it in a staging table.

**Data Extraction Strategy:**
Use incremental extraction to pull only new or updated records based on timestamps eg:(Order_Date, Shipping_Date,’_az_update_ts’,’_az_insert_ts’).
Make API calls at regular intervals to ensure the most recent shipment statuses are captured.
#### 3. Data Transformation
The transformation step involves:
#### Data Cleansing:
Dropping  duplicates (based on Customer_ID or Order_ID).
Handled missing or null values (e.g., shipping status, order amounts).
Handled special characterises (e.g., Frist name status, last name).
Standardized text fields 
#### Joining Tables:
Customer with Shipping: Join on Customer_ID to obtain the shipping status for each order.
(Customer with Shipping)join with Orders: Join on Customer_ID to get each customer’s order details.

#### Derived Columns and Calculations:
1. Total Amount Spent and Country for the Pending Delivery Status for Each Country
Objective: Calculated the total monetary value of transactions for orders that are still in a "Pending" delivery status and aggregate this by each country.
Approach:
Filtered the dataset to include only records with the "Pending" delivery status. Grouped data by Country to summarize the Total_Amount for pending orders.Output a result showing each country and the corresponding total pending amount.
2. Total Number of Transactions, Total Quantity Sold, and Total Amount Spent for Each Customer, Along with Product Details
Objective: For each customer, need to calculate:
Total number of transactions they have made. Total quantity of products they have purchased (even though there is no explicit quantity column, we need to calculate it based on order data or product counts). Total monetary value of all their transactions. Include details about the products they purchased.
Approach:
Group data by Customer_ID and aggregating:
Count the number of orders per customer (total transactions). Calculate total Total_Amount spent by each customer.Determine the total quantity sold using derived logic if Quantity is absent.Use joins to bring in product details (such as Product_Name and Product_ID).The result would be a table of customers, with their transaction totals, amounts, and products purchased.
3. The Maximum Product Purchased for Each Country
Objective: Identified the product that has been purchased the most in each country, based on the total quantity or number of transactions.
Approach:
Grouped data by Country and Product_ID, and count how many times each product was purchased (or infer quantity).For each country, rank or order the products by the count of purchases or quantity sold.Extract the top-ranked (maximum purchased) product for each country.Output the product name and the total count/quantity for that country.
4. The Most Purchased Product Based on Age Category (Less than 30 and Above 30)
Objective: Determine which product is the most popular for two distinct age groups: customers aged less than 30 and those aged 30 and above.
Approach:
First, create a derived column categorizing customers into two age groups: <30 and >=30.Group the data by Age_Category and Product_ID, and count the number of times each product was purchased. For each age group, rank or order the products by their purchase count.Extract the top-ranked (most purchased) product for each age category.
5. The Country That Had the Minimum Transactions and Sales Amount
Objective: Identify the country that has the lowest number of transactions and the least amount of total sales.
Approach:
Group the data by Country, and aggregate:
Count the total number of transactions (orders) per country.Sum up the Total_Amount for each country to get the total sales amount.Rank the countries based on the number of transactions and total sales.Extract the country with the lowest transaction count and sales amount.

Transformation Logic:
Used PySpark for distributed processing.
Implemented transformations using DataFrame APIs such as groupBy, agg, join, and filter.

#### 4. Data Loading:

The transformed data will be loaded into the following target tables in the data warehouse (e.g., Azure Storges account):
#### Fact Tables:
Orders_Fact(temp_view): Contains the final order data, including customer and product details, total amount spent, and shipping status.
Dimension Tables:
 	Customer_Dim(temp_view): Enriched customer data, including demographic details like age and country.
Shipping_Dim(temp_view):Contains shipping information, including status and tracking.
Data Loading Strategy:
Incremental Loading: 
Only new or updated records should be loaded to avoid duplication.Batch or Stream Processing: Depending on the size and velocity of the data, implement batch loads (daily) or real-time stream loads (for APIs).
Indexes: 
Create indexes on frequently queried columns (Customer_ID, Order_ID) to optimize query performance.

5. Data Validation and Testing:
To ensure data accuracy and reliability, implement the following validation checks:

Data Completeness:
Verify that all expected fields are populated (e.g., Customer_ID, Order_Date, Total_Amount).
Data Integrity:
Ensure that joins between tables (e.g., Customer_ID in Orders and Customers) result in correct and complete data.
Business Logic Validation:
Ensure that calculated fields (e.g., total sales, most purchased Item) are consistent with source data.
Unit Tests:
Create unit tests for key transformations to ensure they produce the expected output.
Validate those filters (e.g., age < 30) work correctly.


6. Performance Optimization
Partitioning:Partition data by Order_Date or Customer_ID for efficient query processing.
Caching:Cache intermediate DataFrames in memory to optimize repeated calculations (e.g., total amount per customer).
Indexing:Index keys such as Customer_ID, and Order_ID in the target warehouse to speed up lookup queries.

V.  Communicating Findings and Insights
Visualization Techniques:
To communicate the insights effectively to stakeholders, you can leverage the following visualization techniques:

Pie Chart: Total Amount Spent for Pending Deliveries by Country
Purpose:
The goal of this pie chart is to show the proportion of total pending amount that each country contributes. This allows stakeholders to quickly see which countries have the largest or smallest pending deliveries.
Key Insights:
Country Contributions:
The size of each slice represents the total pending delivery amount for that country as a proportion of the overall pending delivery total.
Larger slices indicate countries with more pending orders in terms of monetary value.
Visual Representation:
Color Coding: Each country is represented by a different color. This makes it easy to distinguish between countries.
Labels: The total pending amount (or percentage share) can be displayed directly on each slice, providing quick access to the exact values.
Example:
Let’s say we have pending delivery data for three countries:
UK: $ 1,36,300 (53.33% of total pending amount)
UAE: $ 53,800 (21.3% of total pending amount)
USA: $65,500 (25.63% of total pending amount)

