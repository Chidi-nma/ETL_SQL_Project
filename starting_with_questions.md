Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

```SQL
SQL Queries:
SELECT country, city, SUM(total_transaction_revenue) AS revenue  
FROM all_sessions
WHERE city != 'not available in demo dataset' 
	AND total_transaction_revenue IS NOT NULL
GROUP BY country, city
ORDER BY revenue DESC
```


Answer:
```
| #  | Country        | City           | Revenue       |
|----|----------------|----------------|----------------|
| 1  | United States  | San Francisco  | 15,643,200,000 |
| 2  | United States  | Sunnyvale      | 9,922,300,000  |
| 3  | United States  | Atlanta        | 8,544,400,000  |
| 4  | United States  | Palo Alto      | 6,080,000,000  |
| 5  | Israel         | Tel Aviv-Yafo  | 6,020,000,000  |
| 6  | United States  | New York       | 5,303,600,000  |
| 7  | United States  | Mountain View  | 4,833,600,000  |
| 8  | United States  | Los Angeles    | 4,794,800,000  |
| 9  | United States  | Chicago        | 4,495,200,000  |
| 10 | Australia      | Sydney         | 3,580,000,000  |
| 11 | United States  | Seattle        | 3,580,000,000  |
| 12 | United States  | San Jose       | 2,623,800,000  |
| 13 | United States  | Austin         | 1,577,800,000  |
| 14 | United States  | Nashville      | 1,570,000,000  |
| 15 | United States  | San Bruno      | 1,037,700,000  |
| 16 | Canada         | Toronto        |   821,600,000  |
| 17 | Canada         | New York       |   679,900,000  |
| 18 | United States  | Houston        |   389,800,000  |
| 19 | United States  | Columbus       |   219,900,000  |
| 20 | Switzerland    | Zurich         |   169,900,000  |
```



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT city, country, ROUND(AVG(sbs.total_ordered)) AS average_number_of_products
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.product_sku = sbs.product_sku
WHERE sbs.total_ordered <> 0 
	AND city <> 'not available in demo dataset' 
	AND city <> '(not set)'
	AND country <>'(not set)'
GROUP BY city, country 	
ORDER BY average_number_of_products DESC

```


Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
-- products that were ordered by visitors
CREATE TEMP TABLE total_products_ordered AS
	SELECT full_visitorid, als.product_sku, v2_productcategory, total_ordered, city, country
	FROM all_sessions als
	JOIN sales_by_sku sbs
	ON als.product_sku = sbs.product_sku
	WHERE sbs.total_ordered <> 0 
		AND city <> 'not available in demo dataset' 
		AND city <> '(not set)'
		AND country <>'(not set)'
	ORDER BY v2_productcategory DESC;

-- to view each category
-- Almost every order is from the home category 
-- consider doing a percentage to show proof
SELECT full_visitorid, product_sku, v2_productcategory, total_ordered, city, country
FROM total_products_ordered
-- WHERE v2_productcategory LIKE '%Home%' 


```



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```SQL
SELECT v2_productname, country, SUM(total_ordered) AS total_orders
FROM (
	SELECT als.product_sku, v2_productname, city, country, total_ordered--, SUM(total_ordered)
	FROM all_sessions als
	JOIN sales_by_sku sbs
	ON als.product_sku = sbs.product_sku
	WHERE sbs.total_ordered <> 0 
		AND city <> 'not available in demo dataset' 
		AND city <> '(not set)'
		AND country <>'(not set)'
	)
GROUP BY v2_productname, country
ORDER BY total_orders DESC
```



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







