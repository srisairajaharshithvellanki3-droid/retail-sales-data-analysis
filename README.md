🛒 Retail Sales Data Analysis (SQL Project)
📌 Overview

This project focuses on analyzing retail sales data using SQL. It covers data cleaning, exploration, and business insights generation through structured queries.

The dataset includes transaction-level details such as customer demographics, product categories, and sales metrics.

🗂️ Database Schema
CREATE TABLE retail_sales
(
    transaction_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
🧹 Data Cleaning

The following steps were performed to ensure data quality:

Checked for NULL values across all columns
Removed records with missing critical fields
DELETE FROM retail_sales
WHERE 
    transaction_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;
🔍 Data Exploration
Key checks:
Total number of sales
Unique customers count
Available product categories
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;
📊 Business Questions & Insights
1️⃣ Sales on a Specific Date

Retrieve all transactions on a given date.

SELECT * 
FROM retail_sales
WHERE sale_date = '2022-11-05';
2️⃣ High-Volume Clothing Sales

Transactions where:

Category = Clothing
Quantity ≥ 4
Month = November 2022
3️⃣ Total Sales by Category
SELECT 
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
4️⃣ Average Age (Beauty Category)
SELECT ROUND(AVG(age), 2)
FROM retail_sales
WHERE category = 'Beauty';
5️⃣ High-Value Transactions
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
6️⃣ Transactions by Gender & Category
SELECT 
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender;
7️⃣ Best Selling Month Each Year
Uses window functions (RANK())
Finds highest average monthly sales per year
8️⃣ Top 5 Customers
SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
9️⃣ Unique Customers per Category
SELECT 
    category,
    COUNT(DISTINCT customer_id)
FROM retail_sales
GROUP BY category;
🔟 Sales by Time Shift

Shifts defined as:

🌅 Morning: Before 12 PM
🌞 Afternoon: 12 PM – 5 PM
🌙 Evening: After 5 PM
CASE
    WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
    WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
    ELSE 'Evening'
END
🛠️ Tools & Technologies
SQL (PostgreSQL / MySQL compatible with minor changes)
Window Functions
Aggregate Functions
Data Cleaning Techniques
🚀 Key Learnings
Writing efficient SQL queries for analysis
Using window functions for ranking
Handling NULL values and data cleaning
Extracting business insights from raw data
📈 Future Improvements
Connect with visualization tools (Power BI / Tableau)
Add stored procedures for automation
Build dashboards for real-time insights
