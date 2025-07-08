## What are your risk areas? Identify and describe them.
> The following are the potential risks
1. Every visitor who has a visitor session should have a time_on_site and pageviews that are greater than zero.
2. The sales report may not contain information about every sale made on the website.  


### QA Process:
> Describe your QA process and include the SQL queries used to execute it.

1. Check that every visitor with a session recorded will have their time on site and page views recorded. 
Answer
> Check for time on site
```SQL
SELECT full_visitorid, time_on_site, pageviews
FROM all_sessions
WHERE time_on_site IS NULL
```
From this query result, we can see that not all visitors with an active session have their time on site recorded. 

> Check that visitors with a unique ID have their pages viewed recorded
```sql
SELECT full_visitorid, time_on_site, pageviews
FROM all_sessions
WHERE pageviews IS NULL
```
From this query result, we can see that every visitor with a session had their page view recorded.

2. Check the number of products with a recorded sale in the sales report table and compare it with the number in the sales_by_sku table
> Check the count in the sales report 
```sql
SELECT COUNT(*)
FROM (
	SELECT distinct product_sku
	FROM sales_report
	WHERE total_ordered <> 0
	ORDER BY product_sku DESC)
```
> RESULT is 304

> Check the count in the sales by sku table
```SQL
SELECT COUNT(*)
FROM (
	SELECT distinct product_sku
	FROM sales_by_sku
	WHERE total_ordered <> 0
	ORDER BY product_sku DESC)
```
> RESULT is 306
From the two results, we can see that the sales by sku table contains 2 products that aren't on the sales table. 
