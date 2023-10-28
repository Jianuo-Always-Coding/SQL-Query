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

### Inserting Hierarchical Rows