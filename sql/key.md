# Key

## Primary Key

> Indicates that a column, or group of columns, can be used as a unique identifier for rows in the table.

```sql
CREATE TABLE products (
    product_no integer UNIQUE NOT NULL,
    name text,
    price numeric
);

CREATE TABLE products (
    product_no integer PRIMARY KEY,
    name text,
    price numeric
);

CREATE TABLE example (
    a integer,
    b integer,
    c integer,
    PRIMARY KEY (a, c)
);
```

* A table can have at most one primary key；
* There can be any number of unique and not-null constraints, which are functionally almost the same thing, but only one can be identified as the primary key;

## Foreign Key

> Maintaining the *referential integrity* between two related tables.

```sql
CREATE TABLE cities (
        city     varchar(80) primary key,
        location point
);

CREATE TABLE weather (
        city      varchar(80) references cities(city),
        temp_lo   int,
        temp_hi   int,
        prcp      real,
        date      date
);

CREATE TABLE t1 (
  a integer PRIMARY KEY,
  b integer,
  c integer,
  FOREIGN KEY (b, c) REFERENCES other_table (c1, c2)
);
```

* It is impossible to create orders with non-NULL foreign key entries that do not appear in the reference table.