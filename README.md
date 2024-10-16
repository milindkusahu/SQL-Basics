# SQL Cheat Sheet

## Basic Query Structure

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1 ASC
LIMIT 10;
```

## Keywords and Clauses

### SELECT

Specifies which columns to retrieve.

```sql
SELECT first_name, last_name FROM employees;
```

### DISTINCT

Removes duplicate rows from the result.

```sql
SELECT DISTINCT department FROM employees;
```

### FROM

Specifies the table to query.

```sql
SELECT * FROM customers;
```

### WHERE

Filters rows based on a condition.

```sql
SELECT * FROM products WHERE price > 100;
```

### ORDER BY

Sorts the result set.

```sql
SELECT * FROM employees ORDER BY last_name ASC;
```

### LIMIT

Restricts the number of rows returned.

```sql
SELECT * FROM top_sellers LIMIT 5;
```

### JOIN

Combines rows from two or more tables.

```sql
SELECT orders.order_id, customers.name
FROM orders
JOIN customers ON orders.customer_id = customers.id;
```

### GROUP BY

Groups rows that have the same values.

```sql
SELECT department, COUNT(*) as employee_count
FROM employees
GROUP BY department;
```

### HAVING

Specifies a search condition for a group or aggregate.

```sql
SELECT department, AVG(salary) as avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### INSERT INTO

Adds new rows to a table.

```sql
INSERT INTO customers (name, email) VALUES ('John Doe', 'john@example.com');
```

### UPDATE

Modifies existing rows in a table.

```sql
UPDATE products SET price = 19.99 WHERE id = 1001;
```

### DELETE

Removes rows from a table.

```sql
DELETE FROM orders WHERE order_date < '2020-01-01';
```

## Aggregate Functions

- COUNT(): `SELECT COUNT(*) FROM employees;`
- SUM(): `SELECT SUM(amount) FROM transactions;`
- AVG(): `SELECT AVG(price) FROM products;`
- MAX(): `SELECT MAX(population) FROM cities;`
- MIN(): `SELECT MIN(temperature) FROM weather_data;`

## Aggregation and Grouping

GROUP BY groups rows with the same values in specified columns and computes summaries for each group.

```sql
SELECT country_id, SUM(population)
FROM city
GROUP BY country_id;
```

```sql
SELECT country_id, AVG(rating)
FROM city
GROUP BY country_id
HAVING AVG(rating) > 3.0;
```

## Subqueries

Subqueries are queries nested inside another query or subquery.

### Single Value Subquery

```sql
SELECT name
FROM city
WHERE rating = (
    SELECT rating
    FROM city
    WHERE name = 'Paris'
);
```

### Multiple Values Subquery

```sql
SELECT name
FROM city
WHERE country_id IN (
    SELECT country_id
    FROM country
    WHERE population > 20000000
);
```

### Correlated Subquery

```sql
SELECT *
FROM city main_city
WHERE population > (
    SELECT AVG(population)
    FROM city average_city
    WHERE average_city.country_id = main_city.country_id
);
```

## Set Operations

Set operations combine results of two or more queries into a single result.

### UNION

Combines results and removes duplicates (UNION ALL keeps duplicates).

```sql
SELECT name FROM cycling WHERE country = 'DE'
UNION
SELECT name FROM skating WHERE country = 'DE';
```

### INTERSECT

Returns only rows that appear in both result sets.

```sql
SELECT name FROM cycling WHERE country = 'DE'
INTERSECT
SELECT name FROM skating WHERE country = 'DE';
```

### EXCEPT

Returns rows from the first result set that don't appear in the second.

```sql
SELECT name FROM cycling WHERE country = 'DE'
EXCEPT
SELECT name FROM skating WHERE country = 'DE';
```

Remember to adjust table names, column names, and values according to your specific database schema and requirements.
