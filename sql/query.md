# Query

## SELECT

```sql
SELECT <columns>
FROM <table>;
```

* Use `*` to return all columns;
* Columns separated by **comma**;
* Ignore hard returns, additional white space, and case insensitive;
* Use **double quote** for columns with a space in its name;

## WHERE

> filters out rows based on boolean logic

```sql
SELECT
FROM
WHERE;
```

* String is **case sensitive**;
* Use **single quote** for string;

## AS

> rename columns / tables

* AS is not required;

## ORDER BY

> sort returned data

```sql
ORDER BY <column> ASC / DESC
ORDER BY <column1> ASC / DESC, <column2> ASC /DESC
```

* Default is ascending;
* `null` values are larger than non-nulls, when numbers; are alphabetically last;
* Sort character data in case insensitive manner;
* Multiple `ORDER BY` sorted sequentially;
* Can order by columns that are not selected;
* When there is `DISTINCT` in `SELECT`, the column being sorted is the same one as the column being made distinct;
* 

## LIMIT

> limit the number of rows returned

```sql
LIMIT <number>
```

* Return arbitrary, rather than top;

* Not fully supported by alll version of SQL: (P19)

  | variant | syntax |
  | ------- | ------ |
  |         |        |
  |         |        |
  |         |        |

* Combine `ORDER BY` and `LIMIT` to return the top X;

## CASE

> conditional logic or control flow

```sql
CASE
	WHEN <condition> THEN <>
	WHEN <condition> THEN <>
	ELSE <>
END AS <new name>

# only handle equality constraints
CASE <column>
	WHEN <constraint> THEN <>
	WHEN <constraint> THEN <>
	ELSE <>
END AS <new name>
```

* `ELSE` is optional, the else values will be `NULL`;
* Database checks the `WHEN` statements in order;
* We can use any statement used in `WHERE` in `CASE`;
* Useful application: use case statement to dealing with divide by zero
* (p35)

## DISTINCT

Remove duplicates from the data that is being returned:

* `DISTINCT` is computationally expensive

## GROUP BY

> combines similar values





## Functions

> SQL functions generally operate on a single row of data

`ABS()`: absolute value

`ROUND(<column>, integer)`:

- Without integer: round to nearest whole number;
- Positive integer: round to that many digits after the decimal place;
- Negative integer: round to that many digits before the decimal place.

`LEAST()` & `GREATEST()`: return the lowest or highest value in a particular set of observations

## String Functions

> we can nest functions

`LEFT(<string>, <number>)` & `RIGHT(<string>, <number>)`: take the left and right characters of a string;

`LOWER()` & `UPPER()`: return a lowercase or uppercase version of a string column

`LENGTH()`: 

`TRIM()`: remove letters from a string

* Default is to remove space;
* `LTRIM()` & `RTRIM()`: trim from only a single side

`||`: put two strings together	

| VARIANT    | SYNTAX     |
| ---------- | ---------- |
| MySQL      | `CONCAT()` |
| MS-SQL     | `+`        |
| PostgreSQL | `||`       |

## Comparison

> used in `WHERE`

Common comparison operations: `=`, `>`, `<`, `<=`, `>=`, `!= / <>`

`BETWEEN()`

```sql
<column> BETWEEN <number/string> AND <number/string>
```

* Inclusive: includes both end points
* String not recommend (p29)

`LIKE()` & `ILIKE()`

> match strings, search for specified patterns within a string

* `ILIKE()` is a case insensitive matching, `LIKE()` is case sensitive matching;
* `%`: matching any string;
* `_`: matching a single string;
* `_` requires a character to be there, however, `%` doesn't;





