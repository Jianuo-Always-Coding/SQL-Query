# SQL Basic

## SELECT

```SQL
SELECT
    last_name,
    first_name,
    points,
    (points + 10) * 100 AS "discount factor"
FROM customers
```

- \* : select all
- AS : change the name
- '' / "" : put name into this, we can use space among name

```SQL
SELECT DISTINCT state
FROM customers
```

- DISTINCT : cut duplicate value in 'state'

```SQL
SELECT *
FROM Customers
WHERE birth_date > '1999-09-23'
```

- WHERE : Select all data which meet the condition
- Do not distinguish upper or lower characters

## AND, OR, NOT

```SQL
SELECT *
FROM Customers
WHERE NOT (birth_date > '1990-01-01' OR points > 1000)
```

## IN

```SQL
SELECT *
FROM Customers
WHERE state IN ('VA', 'FL', 'GA')
-- WHERE state NOT IN ('VA', 'FL', 'GA')
```

## BETWEEN

```SQL
SELECT *
FROM Customers
WHERE points BETWEEN 1000 AND 3000
-- WHERE points >= 1000 AND points <= 3000
```

- BETWEEN : included the two range values

## LIKE

```SQL
SELECT *
FROM Customers
WHERE address LIKE '%trail%' OR
      address LIKE '%avenue%'
-- WHERE points >= 1000 AND points <= 3000
```

- '%' : represant any length of characters
- '\_y' : one underLine represent single character

## REGEXP

```SQL
SELECT *
FROM Customers
WHERE last_name REGEXP '^field|mac|rose$'
WHERE last_name REGEXP '[abc]d'  -- ad/bd/cd in last_name

-- WHERE points >= 1000 AND points <= 3000
```

- ^ represent start
- $ represent end
- [] : [a-d] = [abcd]

## IS NULL & IS NOT NULL

```SQL
SELECT *
FROM Customers
WHERE phone_number IS NULL
```

## ORDER BY

```SQL
SELECT first_name, last_name, 10 AS points
FROM Customers
-- ORDER BY first_name DESC, last_name DESC
ORDER BY first_name, last_name
-- ORDER BY 1, 2
```

- When first_name is the same, the consider last_name
- 1, 2 represent the number of column selected

## LIMIT

```SQL
SELECT *
FROM Customers
-- LIMIT 100
LIMIT 6, 3
```

- LIMIT 100 : Restrict the number of the reuslt is 100.
- LIMIT 6, 3 : skip 6 results and then find 3
- <mark>LIMIT always at the end</mark>

## USING

```SQL
SELECT *
FROM sql_store.order_items oi
JOIN products p
    -- ON oi.product_id = p.product_id
    USING (product_id)
```
