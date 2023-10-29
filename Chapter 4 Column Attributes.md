# Column Attributes

How to insert update and delete data.

> - PK : primary key. Identity each data, is unique.
> - NN : not null. This column value can not be null.
> - AI : Auto increment. (自增，usually used in PK)

## INSERT

### Insert a line

When we need to insert a row in a table, we need to see the attributes of columns, and then add.

```SQL
INSERT INTO customers
VALUES (
	DEFAULT,
    'John',
    'Smith',
    '1990-01-01',
    NULL,
    'address',
    'city',
    'CA',
    DEFAULT
)
```

```SQL
INSERT INTO customers (
	first_name,
    last_name,
    birth_date,
    address,
    city,
    state)
VALUES (
    'John',
    'Smith',
    '1990-01-01',
    'address',
    'city',
    'CA')
```

- They are the same.

### Insert multiple lines in a table

```SQL
INSERT INTO shippers (name)
VALUES ('shipper1'),
       ('shipper2'),
       ('shipper3')
```

### Insert Hierarchical Rows

```SQL
INSERT INTO orders (customer_id, order_date, status)
VALUES (1, '2019-01-02', 1);

INSERT INTO order_items
VALUES
	(LAST_INSERT_ID(), 1, 1, 2.95),
    (LAST_INSERT_ID(), 2, 1, 3.95)
```

- Here **LAST_INSERT_ID()** represent last insert Id. In this case should be the upper operation ID.

## CREATE

### Creating a copy of a table.

```SQL
CREATE TABLE order_archived AS
SELECT * FROM orders
```

- Copy all from 'orders' table.
- <mark>But just copy the data, not including the attributes, like PK, AI.</mark>

```SQL
INSERT order_archived
SELECT * FROM orders
WHERE order_date < '2019-01-01' OR payment_date IS NOT NULL 
```
- Add some data into an empty table.
- <mark>"IS NOT NULL" rather than "!= null"</mark>

## UPDATE
### Update a single row

```SQL
UPDATE invoices
SET payment_total = 10, payment_date = '2019-03-01'
WHERE invoice_id = 1
```

### Update multiple rows
```SQL
UPDATE invoices
SET 
	payment_total = invoice_total * 0.5, 
    payment_date = due_date
WHERE client_id IN (3, 4)
```

- WHERE query can be omited, if you don't write that, just update the whole table.


### Using subqueries in updates

```SQL
UPDATE invoices
SET 
	payment_total = invoice_total * 0.5,
	payment_date = due_date
WHERE client_id IN (
            SELECT client_id
            FROM clients
            WHERE state IN ('CA', 'NY'))     
```

```SQL
UPDATE orders
SET comments = 'GOLD CUSTOMER'
WHERE customer_id IN (
				SELECT customer_id
				FROM customers
				WHERE points >= 3000)
```
- Because the select condition will return multiple results, so we need to use 'IN' for 'client_id'.

## DELETE

```SQL
DELETE FROM invoices
-- WHERE invoice_id = 1
```
- Delete all the data in 'invoices' table. So we need to add 'WHERE' condition.