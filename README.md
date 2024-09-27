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

