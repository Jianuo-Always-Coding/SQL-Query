# ARRREGATE FUNCTIONS

> - MAX()
> - MIN()
> - AVG()
> - SUM()
> - COUNT()

```SQL
SELECT
	MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(invoice_total) AS number_of_invoices,
    COUNT(payment_date) AS count_of_payments,
    COUNT(*) AS total_records,
    COUNT(DISTINCT client_id) AS total_distinct__records
FROM invoices
WHERE invoice_date > '2019-07-01'
```

```SQL
SUM(invoice_total * 1.1) AS total
```

- first do multiply for each value, then do sum

```SQL
COUNT(*) AS total_records,
COUNT(DISTINCT client_id) AS total_distinct__records
FROM invoices
```

- COUNT cannot add NULL
- COUNT(\*) : count the total number of records
- DISINCT : add different client_id

## GROUP BY

```SQL
SELECT
	client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
WHERE invoice_date >= '2019-07-01'
GROUP BY client_id
ORDER BY total_sales DESC
```

```SQL
SELECT
	state,
    city,
    SUM(invoice_total) AS total_sales
FROM invoices i
JOIN clients USING (client_id)
GROUP BY state, city
```

```SQl
SELECT
    date,
    pm.name AS payment_method,
    SUM(amount) AS total_payments
FROM payments p
JOIN payment_methods pm
    on p.payment_method = pm.payment_method_id
GROUP BY date, payment_method -- m * n
ORDER BY date
```

## HAVING

```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales,
    COUNT(*) AS number_of_invoices
FROM invoices
GROUP BY client_id
HAVING total_sales > 500 AND number_of_onvoices > 5
```

- 'WHERE' can help us select the data which meet the requirement before 'GROUP BY'.
- 'HAVING' can help us select the data which meet the requirement after 'GROUP BY'.
- The conditions in 'HAVING' must be in SELECT sentence.

## WItH ROLLUP

```SQL
SELECT
	client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id WITH ROLLUP
```

```SQL
SELECT
	state,
    city,
    SUM(invoice_total) AS total_sales
FROM invoices i
JOIN clients c USING (client_id)
GROUP BY state, city WITH ROLLUP
```

- 'WITH ROLLUP' use with 'GROUP BY' can get SUM of each group, and it won't do sum with self-increasing sequence.
  -For the second example, we can see the sum of (states and cities), (states) and (total).
