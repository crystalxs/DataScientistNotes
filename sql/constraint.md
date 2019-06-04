# Constraints

## Check Constraints

> Specify that the value in a certain column must satisfy a Boolean (truth-value) expression.

```sql
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CONSTRAINT positive_price CHECK (price > 0)
);

CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CHECK (price > 0),
    discounted_price numeric CHECK (discounted_price > 0),
    CHECK (price > discounted_price)
);
```

## Not-Null Constraints

> Specifies that a column must not assume the null value.

```sql
CREATE TABLE products (
    product_no integer NOT NULL,
    name text NOT NULL,
    price numeric
);
```

## Unique Constraints

> Ensure that the data contained in a column, or a group of columns, is unique among all the rows in the table.

```sql
CREATE TABLE products (
    product_no integer UNIQUE,
    name text,
    price numeric
);

CREATE TABLE example (
    a integer,
    b integer,
    c integer,
    UNIQUE (a, c)
);
```