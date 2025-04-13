# Digital-Store-Analysis-SQL-
 Data Analyst Internship – Task 3: SQL for Data Analysis

 Objective
Use SQL queries to extract, manipulate, and analyze structured data from an e-commerce dataset.


 Tools Used
 MySQL (can also use PostgreSQL or SQLite)
 
 Dataset
**Ecommerce Sales Data**

Sample columns include:
- `Order ID`
- `Product`
- `Quantity Ordered`
- `Price Each`
- `Order Date`
- `Purchase Address`

---

 What I Did
Data Cleaning & Formatting**
   - Parsed date & time correctly using `STR_TO_DATE()`.
   - Extracted `Month`, `Hour`, and `State` from `Order Date` and `Purchase Address`.

Key Business Questions Answered**
   -  Top 5 Best-Selling Products  
   -  Least 5 Selling Products  
   - Monthly Revenue Trends  
   -  Hourly Purchase Trends  
   - State-wise Order Distribution  
   -  Average Revenue Per User  
   - Subqueries for filtering top performers  
   -  Created views for clean reusability

SQL Concepts Used**
   - `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`
   - `INNER JOIN`, `LEFT JOIN`
   - Aggregate functions: `SUM()`, `AVG()`, `COUNT()`
   - `HAVING` vs `WHERE`
   - Subqueries
   - Date and time extraction
   - Query optimization using indexing
   - View creation

---

 Sample Queries
 Top 5 Best-Selling Products:
```sql
SELECT Product, COUNT(`Quantity Ordered`) AS Order_Count
FROM updated_sales
GROUP BY Product
ORDER BY Order_Count DESC
LIMIT 5;

State Wise Count
SELECT 
    SUBSTRING_INDEX(SUBSTRING_INDEX(`Purchase Address`, ',', -1), ' ', 2) AS State,
    COUNT(*) AS Total_Orders
FROM updated_sales
GROUP BY State
ORDER BY Total_Orders DESC;

SELECT 
    MONTHNAME(STR_TO_DATE(`Order Date`, '%m/%d/%y %H:%i')) AS Month,
    SUM(`Quantity Ordered` * `Price Each`) AS Revenue
FROM updated_sales
GROUP BY Month
ORDER BY Revenue DESC;


Interview Questions
1. What is the difference between WHERE and HAVING?
WHERE filters rows before aggregation.
HAVING filters after aggregation (like after GROUP BY).

2. What are the different types of joins?
INNER JOIN: Matches in both tables.
LEFT JOIN: All records from the left + matched from the right.
RIGHT JOIN: All from right + matched from left.
FULL OUTER JOIN: All records from both tables (not supported in MySQL directly).
CROSS JOIN: Cartesian product.

3. How do you calculate Average Revenue Per User?
sql
Copy
Edit
SELECT SUM(revenue) / COUNT(DISTINCT user_id) AS ARPU
FROM transactions;

4. What are subqueries?
Subqueries are nested queries inside another query. Example:

sql
Copy
Edit
SELECT name 
FROM employees 
WHERE department_id IN (SELECT id FROM departments WHERE location = 'NY');


5. How do you optimize SQL queries?
Use indexes

Avoid SELECT *
Use EXPLAIN for performance insight
Reduce nested queries
Filter early with WHERE


6. What is a view in SQL?
A view is a virtual table generated from a query.

sql
Copy
Edit
CREATE VIEW popular_products AS
SELECT Product, COUNT(*) FROM sales GROUP BY Product;


7. How do you handle NULL values?
Use IS NULL, IS NOT NULL
Replace with default using COALESCE() or IFNULL()
Handle in aggregation using COUNT(column) (ignores NULLs)



