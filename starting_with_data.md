Question 1: 
> What products did visitors look at btw November 2016 and December 2016 and were ordered, and how many times was the product viewed in total, as well as the amount of time spent looking at each product?
  

SQL Queries:
```sql
SELECT v2_productname, 
	SUM(total_ordered) AS total_orders, 
	SUM(als.pageviews) AS page_views, 
	SUM(als.time_on_site) AS time_on_site
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.product_sku = sbs.product_sku
WHERE sbs.total_ordered <> 0 
	AND city <> 'not available in demo dataset' 
	AND city <> '(not set)'
	AND country <>'(not set)'
	AND (date BETWEEN '2016-11-01' AND '2016-12-31')
	AND time_on_site IS NOT NULL
GROUP BY v2_productname
ORDER BY total_orders DESC
LIMIT 10
```

Answer: 



Question 2: 

SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
