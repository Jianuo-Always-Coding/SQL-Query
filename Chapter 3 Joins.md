# INNER JOINS

```SQL
SELECT order_id. orders.customer_id, first_name, last_name
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
```

```SQL
SELECT order_id. o.customer_id, first_name, last_name
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
```

- This action combine the two table 'orders' and 'customers' together.
- When you select a column which both in the two tables, you must claim which column it from, like orders.customer_id.

## JOINING ACROSS DATABASES

```SQL
SELECT *
FROM sql_store.order_items oi
JOIN products p
    ON oi.product_id = p.product_id
```

- connect with other databases

## SELF JOINS

```SQL
USE sql_hr;

SELECT e.employee_id, e.first_name, m.first_name AS manager
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id
```

- FROM and JOIN the same table

## JOINING MULTIPLE TABLES

```SQL
USE sql_store;

SELECT
	o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.name
FROM orders o
JOIN customers c
	ON o.customer_id = c. customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id
```

- JOIN different tables in the same database.
- We can use "AND" to add other condition in "ON".

## IMPLICIT JOIN SYNTAX

```SQL
SELECT *
FROM  orders o
JOIN customers c
    ON o.customer_id = c.customer_id
```

```SQL
SELECT *
FROM orders o, customers c
WHERE o.customer_id = c.customer_id
```

- They are the same. But we try not to use the second method.

# OUTER JOINS

```SQL
SELECT c.customer_id,
    c.first_name,
    o.order_id
FROM  orders o
LEFT JOIN customers c
-- FROM customers c
-- RIGHT JOIN orders o
    ON o.customer_id = c.customer_id
ORDER BY c.customer_id
```

- If not all data in the 'FROM' table are suit the 'ON' condition, we don't want to lose data. So we use 'Outer Joins'.
- The two ways of LEFT and RIGHT are the same.
- When we use 'LEFT', we keep the 'FROM' table, and add other information from 'LEFT JOIN' table.
- When we use'RIGHT', we keep the 'RIGHT JOIN' table, and add other information from 'FROM' table.

## OUTER JOINS BETWEEN MULTIPLE TABLES

```SQL
SELECT c.customer_id,
	c.first_name,
    o.order_id,
    sh.name AS shipper
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.customer_id
LEFT JOIN shippers sh
	ON sh.shipper_id = o.shipper_id
ORDER BY c.customer_id
```

- Here I used two outer joins. If I turn the second join function into inner join(delete 'LEFT'), we can not get all the customers in 'customer' table.
- Avoid to use 'RIGHT JOIN'

## SELF OUTER JOINS

```SQL
SELECT
	e.employee_id,
	e.first_name,
    m.first_name AS managera
FROM employees e
LEFT JOIN employees m
	ON e.reports_to = m.employee_id
```

## NATURAL JOINS

```SQL
SELECT
    o.order_id,
    c,first_name
FROM orders o
NATURAL JOIN customers c
```

- 'NATURAL JOIN' can auto select the column which have the same name as the join condition.
- Do not recommend.

## CROSS JOINS

```SQL
SELECT
	c.first_name AS customer,
    p.name AS product
FROM customers c
CROSS JOIN products p
-- FROM customers c, products p
ORDER BY c.first_name
```

- This operation can list all combinations with 2 forms.(m \* n)
- There are two ways to use this, but I think the explicit syntax is the most clearly.

## UNION

```SQL
SELECT
	order_id,
    order_date,
    'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'

UNION

SELECT
	order_id,
    order_date,
    'Actived' AS status
FROM orders
WHERE order_date < '2019-01-01'
```

- Use 'UNION', we can combine several results together.
```SQL
SELECT first_name
FROM archived_orders
UNION
SELECT name
FROM orders
```
- Also the reuslts could not in the same table. But we must ensure that the numbers of columns are the same.
- The columns' names depend on the first part result.
