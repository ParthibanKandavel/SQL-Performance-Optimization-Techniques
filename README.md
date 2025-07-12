# SQL-Performance-Optimization-Techniques

## 1. Use Proper Indexing
```sql
CREATE INDEX idx_customer_id ON sales_data(customer_id);
```
Use indexes on columns used in `JOIN`, `WHERE`, and `ORDER BY` clauses.

## 2. Avoid SELECT *
```sql
SELECT customer_id, order_date FROM orders;
```
Select only required columns to reduce I/O.

## 3. Use EXISTS Instead of IN (for correlated subqueries)
```sql
-- Instead of this:
SELECT * FROM orders WHERE customer_id IN (SELECT customer_id FROM customers);

-- Use this:
SELECT * FROM orders o WHERE EXISTS (
  SELECT 1 FROM customers c WHERE c.customer_id = o.customer_id
);
```

## 4. Use LIMIT or TOP for Large Data
```sql
SELECT * FROM large_table LIMIT 100;
```
Helps in debugging and paginating results.

## 5. Use CTEs for Modular Queries
```sql
WITH recent_orders AS (
  SELECT * FROM orders WHERE order_date > CURRENT_DATE - INTERVAL '30 day'
)
SELECT customer_id, COUNT(*) FROM recent_orders GROUP BY customer_id;
```

## 6. Analyze and Tune with EXPLAIN
```sql
EXPLAIN SELECT * FROM orders WHERE customer_id = 1001;
```
This helps understand index usage, joins, and bottlenecks.

## 7. Partition Large Tables
```sql
CREATE TABLE sales_partitioned (
  sale_id INT,
  region VARCHAR,
  sale_date DATE
)
PARTITION BY RANGE (sale_date);
```
Improves query performance on filtered ranges.

---

Feel free to modify this template to suit your enterprise RLS, ETL performance, and SQL tuning needs.
