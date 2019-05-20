# Types

> Relational databases are strongly or statically typed.

## Numbers

### Integer

### Float

###Numeric Type

> Having fixed cut-off precision.

###Division

Dividing an integer by another integer, the database attempt to do integer math and it will concatenates the data.

```sql
SELECT registrations * 1.0 / 10
FROM cls.cars;

SELECT registrations / 10.0
FROM cls.cars;

# PostgreSQL specific
SELECT registrations::float / 10
FROM cls.cars;
```

## String

### Variable Length

`varcha(<length>)`

### Fixed Length

`char`

###Arbitrary Length

`text`

## Dates

`Dates`

`Time`

`Timestamp` (`datetime`)

`Interval`

### Dates Functions

`now()`: returns the current timestamp;

`current_date` and `current_time`: returns the current date and time; where `current_time` is full timestamp;

`date_part()` (`extract()`): extracts a particular part of the date or timestamp;

* `date_part('month', '2012/03/12'::date)`;
* `month`, `hour`, `dow` (start with Sunday at zeros and goes to Saturday as 6);

`date_trunc()`: truncates a date or timestamp down to a certain precision

* will return a timestamp with the values beyond the specified precision set to their lowest possible value;

`date()`: return the date of a given timestamp in date format;

Using interval to add and subtract time information.

## Cast Operator

> Switching data types.

* Using the `::` operator (PostgreSQL specific);

* In most SQL variants:

  ```sql
  SELECT CAST( registrations as float)/10
  FROM cls.cars;
  ```

## `NULL`

> Relational databases have 3-value logic: True, False, and NULL (missing).

* `NULL`s never evaluate `True`, only `False`;
  * even `NULL=NULL` evaluates `False`;
* Using `IS NULL` to compare `NULL`;
* Using `IS NOT NULL` to remove`NULL` values;
* `NULL` values are larger than non-nulls, when numbers; are alphabetically last;
* `WHERE annualfee <> 0` will also remove `NULL` values;
* 