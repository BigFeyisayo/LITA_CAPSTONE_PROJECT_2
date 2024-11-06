# LITA_CAPSTONE_PROJECT_2
INCUBATOR HUB: This repository contains a comprehensive Customer Segmentation Analysis for a subscription service. Using Excel, SQL, &amp; PowerBI for my analysis &amp; report.

### Project Title: Customer Segmentation Analysis

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools And Technologies](#tools-and-technologies)

[Data Cleaning And Preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)


### Project Overview
---
This project is a comprehensive analysis of customer data aimed to identify segments, track subscription types, and analyze trends in cancellations and renewals. The goal is to develop insights to inform business decisions, improve customer retention, and optimize subscription offerings.

### Data Sources
---
The primary source of data used here is LITA Capstone Dataset.xlsx. 

### Tools And Technologies
---
- Microsoft Excel: 
  1. For data analysis and visualization.
  2. For data summarization and pivot tables.
  3. To create charts and reports.

- Structured Query Language - SQL: 
  1. To retrieve and analyze data.
  2. To manage and manipulate the data
  3. To create, query, and modify the data.

- PowerBI:
  1. For data visualization and reporting.
  2. For data modeling and transformation.
  3. To create interactive dashboards.

### Data Cleaning And Preparation
---
It is crucial to clean and get data ready for exploration. In order to do this, I performed the following:

- Identified & removed duplicate records using [the 'remove duplicate tool' from the data tab]
- Normalized the dataset by;
    - Standardizing the date formats to [format, e.g., YYYY-MM-DD].
    - Converting each columns' data type.
    - Filtering the columns.
    - Adding columns I deemed fit.

### Exploratory Data Analysis
---
This involves the exploration of data to answer the following questions:
- Average Revenue Per User

![EDA-ARPU](https://github.com/user-attachments/assets/d4ab9c36-2cce-4576-b8c3-06d93de41382)

- Subscription Type By Revenue

![EDA-Sub_Type_By_Revenue](https://github.com/user-attachments/assets/0a9c351c-6d0d-44f7-81ac-a872a7a0d0d9)

- What is the average subscription duration?

![EDA-Avr_Sub_Duration](https://github.com/user-attachments/assets/48fa04f0-817f-4b00-afff-c9177fdc3853)

- What is the most popular subscription type?
  
![EDA-Most_pop_sub_type](https://github.com/user-attachments/assets/2fc61889-0091-4c82-ab70-c236b24253c4)

### Data Analysis
---
Line of queries/codes used during analysis.

- Retrieve the total number of customers from each region.
```SQL
Select
	Region,
	Count(CustomerID) AS TotalCustomers
FROM
	CustomerData
GROUP BY 
	Region
```

- Find the most popular subscription type by the number of customers.
```SQL
Select
	SubscriptionType,
	Count(CustomerID) AS CustomerCount
FROM
	CustomerData
GROUP BY
	SubscriptionType
```

- Find customers who canceled their subscription within 6 months.
```SQL
SELECT 
	CustomerName,
	Canceled,
	SubscriptionStart
FROM 
	CustomerData
WHERE 
	Canceled = 0 AND MONTH(SubscriptionStart) <=6
```

- Calculate the average subscription duration for all customers.
```SQL
Select
	AVG(DATEDIFF(DAY, SubscriptionStart, SubscriptionEnd)) AS AverageDuration
FROM
	CustomerData
```

- Find customers with subscriptions longer than 12 months.
```SQL
Select 
	CustomerID,
	CustomerName,
	SubscriptionType
FROM
	CustomerData
WHERE
	DATEDIFF(day, SubscriptionStart, SubscriptionEnd) > 365
```

- Calculate total revenue by subscription type.
```SQL
Select 
	SubscriptionType,
	SUM(Revenue) AS TotalRevenue
FROM
	CustomerData
GROUP BY SubscriptionType
```

- Find the top 3 regions by subscription cancellations.
```SQL
Select
	TOP 3
	Region,
	COUNT(CustomerID) AS CancellationCount
FROM
	CustomerData
WHERE
	SubscriptionEnd IS NOT NULL
GROUP BY 
	Region
ORDER BY
	CancellationCount DESC
```

- Find the total number of active and canceled subscriptions.
```SQL
SELECT 
	Canceled,
	SUM(CASE WHEN Canceled IS NULL THEN 1 ELSE 0 END) AS ActiveSubscriptions,
	SUM(CASE WHEN Canceled IS NOT NULL THEN 1 ELSE 0 END) AS CanceledSubscriptions
FROM 
	CustomerData
GROUP BY
	CustomerID
```

### Data Visualization

![CustomerData Dashboard](https://github.com/user-attachments/assets/3b692215-6f93-43fd-9260-414148320f75)
