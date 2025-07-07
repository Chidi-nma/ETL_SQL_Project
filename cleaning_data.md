# What issues will you address by cleaning the data?
> The issues that will be addressed in the process of cleaning this data include 
1. Converting the unit price amount in the analytics table to its actual value by dividing by 1,000,000. 
2. Convert the data in the total_transaction_revenue column in the all sessions table to its true value.
3. Removing rows with "not available in the dataset" and "(not set)" from the city and country column in the all sessions table.
4. Remove rows where total transaction revenue is NULL and transactions are NULL from the all sessions table. 





## Queries:
Below, provide the SQL queries you used to clean your data.
> 1. Convert data in the unit price column in the analytics table to unit price. 

```SQL
SELECT *, (unit_price / 1000000)::integer AS true_unit_price
FROM analytics
```

> 2. Convert the data in the total_transaction_revenue column in the all sessions table to its true value.
```sql
SELECT total_transaction_revenue, (total_transaction_revenue / 1000000)::integer AS true_total_revenue
FROM all_sessions
WHERE total_transaction_revenue IS NOT NULL 

```

> 3. Remove any rows with city as 'not available in demo dataset', country, and city as "(not set)"

```SQL
SELECT *
FROM all_sessions
WHERE city <> '(not set)'
	AND country <>'(not set)'
	AND city <> 'not available in demo dataset' 
```

> 4. Remove rows from the sessions table where the total transaction revenue and transactions are null. This allows us to focus on visitors who generated revenue after visiting the site

```
SELECT * 
FROM all_sessions
WHERE total_transaction_revenue IS NOT NULL 
	AND transactions IS NOT NULL
```