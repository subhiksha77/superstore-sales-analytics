-- Superstore Sales Analysis | MySQL 8+
-- Review the schema/import steps before running analytical queries.
-- Source workbook has 5,901 rows and 23 columns; see README for data-quality notes.

CREATE DATABASE IF NOT EXISTS sales;
USE sales;
#total sales
SELECT SUM(Sales) AS Total_Sales
FROM sales;

#total profit
SELECT SUM(Profit) AS Total_Profit
FROM sales;

#which category generate the higher sales
SELECT Category, SUM(Sales) AS Total_Sales
FROM sales
GROUP BY Category
ORDER BY Total_Sales DESC;

-- Which region generates the highest sales?
SELECT Region, SUM(Sales) AS Total_Sales
FROM sales
GROUP BY Region
ORDER BY Total_Sales DESC;

#what are the top 10best-selling products
SELECT `Product Name`, SUM(Sales) AS Total_Sales
FROM sales
GROUP BY `Product Name`
ORDER BY Total_Sales DESC
LIMIT 10;

#which state has the highest sales
SELECT State, SUM(Sales) AS Total_Sales
FROM sales
GROUP BY State
ORDER BY Total_Sales DESC;

#what are the monthly sales trend
SELECT
    DATE_FORMAT(`Order Date`, '%Y-%m') AS Month,
    SUM(Sales) AS Total_Sales
FROM sales
GROUP BY Month
ORDER BY Month;

#which subcatogory generates te highest profit
SELECT `Sub-Category`,
       SUM(Profit) AS Total_Profit
FROM sales
GROUP BY `Sub-Category`
ORDER BY Total_Profit DESC;

#which customer generates the highest sales
SELECT `Customer Name`,
       SUM(Sales) AS Total_Sales
FROM sales
GROUP BY `Customer Name`
ORDER BY Total_Sales DESC
LIMIT 10;

#which shipping mode is most frequently used
SELECT `Ship Mode`,
       COUNT(*) AS Total_Orders
FROM sales
GROUP BY `Ship Mode`
ORDER BY Total_Orders DESC;

#which product are generating losses
SELECT `Product Name`,
       SUM(Profit) AS Total_Profit
FROM sales
GROUP BY `Product Name`
HAVING SUM(Profit) < 0
ORDER BY Total_Profit ASC;

#which customer segment generate the highest sales
SELECT Segment, SUM(Sales) AS Total_Sales
FROM sales
GROUP BY Segment
ORDER BY Total_Sales DESC;

#what is the total quantity sold by category
SELECT Category,
       SUM(Quantity) AS Total_Quantity
FROM sales
GROUP BY Category
ORDER BY Total_Quantity DESC;

#how do discount or returns affect sales
SELECT Returns, COUNT(*) AS Total_Records
FROM sales
GROUP BY Returns;

#which product has higher sales but low profit
SELECT `Product Name`,
       SUM(Sales) AS Total_Sales,
       SUM(Profit) AS Total_Profit
FROM sales
GROUP BY `Product Name`
HAVING SUM(Sales) > 1000
   AND SUM(Profit) < 100
ORDER BY Total_Sales DESC;
