What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

-- gives 462 rows to check distinct SKUs
SELECT distinct product_sku
from sales_by_sku

-- Check to see if there are any null values
SELECT COUNT(*)
FROM sales_by_sku