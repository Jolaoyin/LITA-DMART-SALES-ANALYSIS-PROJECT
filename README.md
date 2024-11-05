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
- Microsoft Power BI: Used to create interactive visual dashboards
- Github: for portfolio building

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
EXCEL FORMULA
AVERAGE SALES PER PRODUCTS
|   PRODUCTS   |             FORMULA                | AVG. SALES|
|--------------|------------------------------------|-----------|
|AVERAGE GLOVES|=AVERAGEIF(C2:C9922,C2,H2:H9922)    |   200.07  |
|AVERAGE HAT   |=AVERAGEIF(C2:C9922,C1486,H2:H9922)	|   158.81  |
|AVERAGE JACKET|=AVERAGEIF(C2:C9922,C4965,H2:H9922)	|   139.94  |
|AVERAGE SHIRT |=AVERAGEIF(C2:C9922,C4965,H2:H9922)	|   326.56  |
|AVERAGE  SHOE |=AVERAGEIF(C2:C9922,C6452,H2:H9922) |   308.70  |
|AVERAGE SOCKS |=AVERAGEIF(C2:C9922,C8439,H2:H9922)	|   121.82  |

TOTAL REVENUE BY REGION	
|REGION| TOTAL REVENUE| FORMULA|
|------|--------------|--------|
|SOUTH |   927,820    |=SUMIF(D2:D9922,D2,H2:H9922    |
|WEST  |   300,345    |=SUMIF(D2:D9922,D3,H2:H9922)   |
|NORTH |   387,000    |=SUMIF(D2:D9922,D1487,H2:H9922)|
|EAST	 |   485,925    |=SUMIF(D2:D9922,D1486,H2:H9922)|
|TOTAL |   2,101,090  |              =SUM(K12:K15)    |

This is where a series of SQL queries is executed to extract key insights from the dataset to facilitate a comprehensice data-driven decision-making. The dataset was loaded into the SQL Server.

```SQL
Create Database LITAProject_DB
```
```
Select * From [dbo].[LITACapstone_Dataset_SalesData]
```
----Totalsales for Each Products
```
Select Product, sum(Total_Sales) as Total_Sales
from [dbo].[LITACapstone_Dataset_SalesData]
Group by Product
```
---Number of Sale Transaction in Each Region
```
Select Region, COUNT(Total_Sales) as Number_of_SalesTransaction
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Region
```
----Highest Selling Product by Total Sales Values
```
Select Top 1 Product, sum(Quantity) as Total_Sales
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Product
Order by Total_Sales DESC
```
---Total Revenue by Product
```
Select Product, SUM(Total_Sales) as TotalRevenue
from [dbo].[LITACapstone_Dataset_SalesData]
Group by Product
```
---Monthly Sales Total for Current Year
```
Select Month(OrderDate) as Month, sum(Total_Sales) as Total_Sales
From [dbo].[LITACapstone_Dataset_SalesData]
Where Year(OrderDate) = Year(Getdate())
Group by Month(OrderDate)
Order by Month(OrderDate);
```
----5 Top Customers by Total Purchase Amount
```
Select Top 5 Customer_Id, sum(Total_Sales) as Total_Sales
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Customer_Id
Order by sum(Total_Sales) Desc
```
---Percentage of Total Sales Contributed by Each Region
```
Select Region, Sum(Quantity) as Total_Sales,
Round ((Sum(Quantity) * 100 /
       Cast((Select Sum(Quantity)  FROM [dbo].[LITACapstone_Dataset_SalesData]) as float)), 2) as Percentage
From [dbo].[LITACapstone_Dataset_SalesData]
Group by Region
Order by Percentage Desc;
```
 ---Products With No Sales In The Last Quarter
 ```
 Select Distinct Product, OrderId, Quantity
 From [dbo].[LITACapstone_Dataset_SalesData]
 Where Product Not In
 (Select distinct Product
 From [dbo].[LITACapstone_Dataset_SalesData]
 Where OrderDate >=DATEADD(Quarter, -1, GETDATE())
 )
 AND OrderDate >=DATEADD(Quarter, -1, GETDATE())
```

## Data Visualisation Using Excel

### Created pivot tables and reports for visualizing the sales data in Excel.
![Pivot Table Sales Data](https://github.com/user-attachments/assets/2f7ce0ca-45d6-4b0a-ad58-98ddbd87630e)

![Sales Report](https://github.com/user-attachments/assets/38b647c7-9a8d-4e7c-a0c8-3ff19b3e856b)


## Data Visualisation Using Power BI for Sales Data

### Steps used to build an interactive PowerBI Dashboard
1. Import and Transform Data: Imported, transformed and loaded sales data.
3. Build Visualizations: Use bar, column,line, donut and pie charts to represent sales data across regions, sales,order dates, products etc.
4. Add KPI and Slicers: Included KPIs for performance tracking and slicers for filtering data by orderdate.
5. Format and Share: Customized the dashboard

![Screenshot sales powerbi](https://github.com/user-attachments/assets/0f3380b5-c2ae-490b-b817-96bb828cfd9a)

## Insights
### Total Sales Performance
- Total Revenue: The Total Revenue is 2 Million.
- Average Total Sales: The average total sales value is 211.78, indicating the average revenue per order.
- Total Quantity and Order Count: A total quantity of 68K products sold across 9,921 orders shows the volume of sales activity.

### Regional Sales
- Total Revenue by Region: From the pie chart in Power BI and pivot table, the West region generates the most revenue (44% or 928K), followed by North (23%) and South (18%), while East contributes the least. This could indicate potential for growth in underperforming regions.
- Average Sales by Region: From the pivot table, West has the highest average sales, suggesting a strong customer base or higher purchasing power in this region.

### Product Performance
1. Top Products by Total Sales and Quantity:
- Shoes are the top product by total sales (613K), followed by Shirts (486K) and Hats (316K).
- The quantity sold chart reveals that Hats have a higher volume of sales but not as high revenue, suggesting a lower price point.
2. Revenue by Product and Region: Shoes perform best across multiple regions, indicating it’s a well-received product, while other products like Jackets and Gloves are more regionally specific.
  
### Sales Trends Over Time
- Monthly Sales Trends: Sales peak in February (546K), then decrease, with slight rises in July and August, showing seasonal fluctuations that could align with customer demand patterns or promotional activities.
- Trend of Total Sales Over Time: The line chart in Power BI highlights peaks in sales during specific months, suggesting possible recurring cycles (e.g., quarterly or bi-annual peaks).
  
### Top Products by Orders
The Top 10 Products by OrderID pivot table shows high-order activity for specific products, with Shoes and Shirts appearing frequently. This suggests that these products may have higher demand or popularity.

## Recommendations
1. Promote More in Low-Sales Regions: Increase advertising or offer discounts in the East and South regions to boost sales.
2. Focus on Best-Selling Products: Keep popular items like Shoes and Shirts well-stocked, and consider creating bundles with other items to increase sales.
3. Run Sales During Slow Months: Offer discounts or special deals in months with lower sales, like March and April, to encourage more purchases.
4. Adjust Inventory Based on Demand: Stock more of the high-demand items in regions where they sell best, and reduce stock of less popular items.
