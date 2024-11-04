# LITA-DMART-SALES-ANALYSIS-PROJECT

## Project Title: Dmart Sales Analysis

## Project Overview
The LITA DMart Sales Analysis and Dashboard Project aims to analyse and visualise DMart's sales performance, delivering actionable insights into customer purchasing patterns, product popularity, and regional sales trends for 2023 and 2024. This project uncovers the key factors influencing the retail store, providing stakeholders with a detailed understanding of growth opportunities and facilitating informed decision-making through data-driven insights.

## Data Sources
The primary source for this analysis is the Sales Data provided by the retail store, which includes key metrics such as OrderID, CustomerID, Product, Region, Order date, Quantity and Unit Price. This comprehensive dataset enables a thorough examination of sales performance and trends.

## Tools Used
- Microsoft Excel: [Download Here](https://www.microsoft.com)
  1. for Data Cleaning
  2. for  Data Transformation 
  3. for Data Analysis
  4. for Data Visualisation

- Structured Query Language (SQL)
- Microsoft Power BI:
 1. Used to create interactive visual dashboards
- Github:
 1. for portfolio building

  ### Data Cleaning and Preparations
  In the initial phase, we perform an initial exploration and summary of the sales data to establish foundational insights:
  1. Removed duplicates and checked for missing values
  2. Generated a new variable by creating a new column "Total Sales" from Unit Price and Quantity.
  3. Validate Data Accuracy
  
## Exploratory Data Analysis
EDA is where Pivot Table, Excel Formulas is used to answer some questions about the data, calculate essential metrics. and highlight unique trends like emerging top selling.
- What is the total sales for each product category?
- What is the number of sales transactions in each region?
- What is the highest selling product bt total sales value?
- What is the total revenue per product?
- What is the monthly sales total for the current year?
- Who are the top 5 customers by total purchase amount?
- What is the total sale percentage for each region?
- Which products has no sales in the last quarter?

## Data Analysis
This is where a series of SQL queries is executed to extract key insights from the dataset to facilitate a comprehensice data-driven decision-making. The dataset was loaded into the SQL Server.

```SQL
Create Database LITAProject_DB

Select * From [dbo].[LITACapstone_Dataset_SalesData]

----Totalsales for Each Products
Select Product, sum(Total_Sales) as Total_Sales
from [dbo].[LITACapstone_Dataset_SalesData]
Group by Product

---Number of Sale Transaction in Each Region
Select Region, COUNT(Total_Sales) as Number_of_SalesTransaction
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Region

----Highest Selling Product by Total Sales Values
Select Top 1 Product, sum(Quantity) as Total_Sales
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Product
Order by Total_Sales DESC

---Total Revenue by Product
Select Product, SUM(Total_Sales) as TotalRevenue
from [dbo].[LITACapstone_Dataset_SalesData]
Group by Product

---Monthly Sales Total for Current Year
Select Month(OrderDate) as Month, sum(Total_Sales) as Total_Sales
From [dbo].[LITACapstone_Dataset_SalesData]
Where Year(OrderDate) = Year(Getdate())
Group by Month(OrderDate)
Order by Month(OrderDate);

----5 Top Customers by Total Purchase Amount
Select Top 5 Customer_Id, sum(Total_Sales) as Total_Sales
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Customer_Id
Order by sum(Total_Sales) Desc

---Percentage of Total Sales Contributed by Each Region
Select Region, Sum(Quantity) as Total_Sales,
Round ((Sum(Quantity) * 100 /
       Cast((Select Sum(Quantity)  FROM [dbo].[LITACapstone_Dataset_SalesData]) as float)), 2) as Percentage
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Region
Order by Percentage Desc;

 ---Products With No Sales In The Last Quarter
 Select Distinct Product, OrderId, Quantity
 From [dbo].[LITACapstone_Dataset_SalesData]
 Where Product Not In
 (Select distinct Product
 From [dbo].[LITACapstone_Dataset_SalesData]
 Where OrderDate >=DATEADD(Quarter, -1, GETDATE())
 )
 AND OrderDate >=DATEADD(Quarter, -1, GETDATE())
```

## Data Visualisation

