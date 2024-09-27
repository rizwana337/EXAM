# Data Analysis and Management Framework for E-commerce

This document provides a comprehensive analysis of sales and customer data, starts with data accuracy check’s, Outline Requirements, Data Modeling Steps. Also Exploring key metrics such as transaction volumes, sales amounts, and purchasing trends across different demographics and regions, while also identifying actionable insights for enhancing customer engagement and driving business growth.

## I. Verify the Accuracy, Completeness, and Reliability of Source Data:
#### * Cross-Referencing: 

Compared the data against known reliable values to validate accuracy and completeness.
Findings are some of the column’s values in Customer table contains Special characters. 

<img width="302" alt="image" src="https://github.com/user-attachments/assets/87e7e4ed-45f6-4606-b3e9-7ad512c13a33">

Fig: 1

Validation Rules: Defined specific validation rules based on the requirements (e.g., acceptable value, data type checks).

#### * Data Profiling:

I have used in-build data profiling feature to analyze the source data for anomalies, missing values, 
duplicates, and inconsistencies.

<img width="434" alt="image" src="https://github.com/user-attachments/assets/ea6cf6cd-81a3-42b7-a941-f3553e787152">

Fig:2. Data profiling for Customer table

<img width="434" alt="image" src="https://github.com/user-attachments/assets/ac1fed62-5caa-41da-af07-7ce225830f3e">

Fig:3. Data profiling for Order table 

<img width="434" alt="image" src="https://github.com/user-attachments/assets/3b9363b7-4861-4600-b8e4-f1a324e03087">

Fig:4. Data profiling for Shipping table


#### . Verified Checklist:

Completeness: Confirmed that all required fields are populated and check for missing records.
Consistency: Validated that data formats are uniform across datasets (e.g., date formats, naming conventions). But some of the column’s values in Customer table contains Special characters.
Timeliness: Assess whether the data is up-to-date and relevant for current analysis needs.

