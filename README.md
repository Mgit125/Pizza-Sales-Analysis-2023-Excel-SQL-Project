![logo](https://github.com/Mgit125/Pizza-Sales-Analysis-2023-Excel-SQL-Project/blob/main/Final%20Pizza%20Sales%20Dashboard.png)

## Project : Pizza Sales Analysis (Excel + SQL)

### Overview

This project delves into a comprehensive analysis of pizza sales data from 2023, aiming to uncover valuable insights into business performance. Utilizing SQL Server and Excel, the project explores key performance indicators (KPIs) to understand sales trends, customer preferences, and operational efficiency.

### Key Objectives

#### Data Analysis: 
Utilize SQL Server to extract and analyze key metrics from the pizza sales data.

#### KPI Calculation: 
Calculate essential metrics such as total revenue, average order value, total pizzas sold, total orders, and average pizzas per order.

#### Trend Identification: 
Identify busiest days, months, quarters, and times to understand peak demand periods.

#### Product Performance: 
Analyze sales performance by pizza category, size, and individual pizza items.

#### Visualization: 
Create an interactive Excel dashboard to visually represent key findings and facilitate data-driven decision-making.

### Methodology

#### Data Import and Database Creation:

Import the CSV/flat file into MS SQL Server.

Create the Pizza_sales_2023_DB database.

Create the Pizza_sales_2023 table with appropriate columns.

### SQL Server Analysis:

Execute SQL queries to calculate KPIs and analyze trends:

Total Revenue

```SQL
SELECT ROUND(SUM(total_price), 2) AS Total_Revenue
FROM Pizza_sales_2023;
```

Average Order Value
```SQL
SELECT ROUND(SUM(total_price) / COUNT(DISTINCT(order_id)), 2)
AS Average_order_value_per_order
FROM Pizza_sales_2023;
```

Total Pizzas Sold
```SQL
SELECT SUM(quantity) AS Total_pizzas_sold
FROM Pizza_sales_2023;
```

Total Orders
```SQL
SELECT COUNT(DISTINCT(order_id)) AS Total_orders
FROM Pizza_sales_2023;
```

Average Pizzas Per Order
```SQL
SELECT CAST(SUM(quantity) AS DECIMAL(10, 2)) /
       CAST(COUNT(DISTINCT(order_id)) AS DECIMAL(10, 2))
FROM Pizza_sales_2023;
```

Busiest Days, Months, Quarters, and Times
```SQL
        --DW for Day of the Week (e.g., 'Monday', 'Tuesday')
				--MONTH for the Month Name (e.g., 'January', 'February')
					--YEAR for the Year (e.g., '2023')
					--DAY for the Day of the Month (e.g., '1', '15', '31')
					--QUARTER for the Quarter (e.g., '1', '2', '3', '4')
-- DAILY TREND IN A WEEK OF PIZZA SALES 
SELECT 
	DATENAME(DW, order_date) AS Order_Day, 
COUNT(DISTINCT order_id) AS total_orders
FROM Pizza_sales_2023
GROUP BY DATENAME(DW, order_date)
ORDER BY COUNT(DISTINCT order_id) DESC;
```
```SQL-- MONTHLY TREND IN A WEEK OF PIZZA SALES 
SELECT 
	DATENAME(MONTH, order_date) AS Order_Month, 
COUNT(DISTINCT order_id) AS total_orders
FROM Pizza_sales_2023
GROUP BY DATENAME(MONTH, order_date)
ORDER BY COUNT(DISTINCT order_id) DESC;
```
```SQL
-- Quarterly TREND OF PIZZA SALES 
SELECT 
	DATENAME(QUARTER, order_date) AS Order_QUARTER, 
COUNT(DISTINCT order_id) AS total_orders
FROM Pizza_sales_2023
GROUP BY DATENAME(QUARTER, order_date)
ORDER BY COUNT(DISTINCT order_id) DESC;
```
```SQL
-- HOURLY TREND OF PIZZA SALES 
	SELECT 
		DATEPART(HOUR, order_time) AS Time_of_order_placed, 
		COUNT(DISTINCT(order_id)) AS total_orders
	FROM Pizza_sales_2023
	GROUP BY DATEPART(HOUR, order_time)
	ORDER BY COUNT(DISTINCT(order_id)) DESC;
```

Sales Percentage by Pizza Category and Size

Total Pizzas Sold by Pizza Category

Top and Bottom Sellers

### Excel Dashboard Creation:

Extract data from SQL Server and import it into Excel.
Clean and format the data.
Calculate additional metrics if needed.
Create visualizations (charts, graphs) to represent key findings.

### Key Findings

#### Revenue: 

Total revenue generated was approximately £817,860.

#### Orders: 

Average order value was £38.31. A total of 21,350 orders were placed in 2023, with an average of 2.32 pizzas per order.

#### Busiest Times: 

Mondays, Tuesdays, Saturdays, and Sundays were the busiest days. Peak order times were between 12-1 PM and 4-8 PM.

#### Sales: 

The "Classic" pizza category and "Large" size pizza contributed the most to sales.

#### Best and Worst Sellers: 

"Classic Deluxe" and "Chicken" pizzas were the best sellers, while "The Brie Carre" performed the worst in terms of both orders and revenue.

### Conclusion

This project provides valuable insights into the pizza business's sales trends, customer preferences, and peak demand periods. These findings can be used to optimize operations, marketing strategies, and inventory management to improve overall business performance.
