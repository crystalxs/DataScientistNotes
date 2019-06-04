# Query

## `SELECT`

```sql
SELECT <column>(s)
FROM <schema>.<table>;
```

* Use `*` to return all columns;
* Columns separated by **comma**;
* Ignore hard returns, additional white space, and case insensitive;
* Use **double quote** for columns with a space in its name.

### `DISTINCT`

> Removing duplicates from the data that is being returned.

- `DISTINCT` is computationally expensive;
- Common error occurred when sort: `DISTINCT` and `ORDER BY` can be used only when the column being sorted is the same one as the column being made distinct.

### `COALESCE`

> Return the first non-Null value it encounters.

If  all values are `NULL`, then a `NULL` is returned.

### `CASE`

> conditional logic or control flow

```sql
CASE
	WHEN <condition> THEN <value>
	WHEN <condition> THEN <value>
	ELSE <value>
END AS <new name>

# only handle equality constraints
CASE <column>
	WHEN <constraint> THEN <value>
	WHEN <constraint> THEN <value>
	ELSE <value>
END AS <new name>
```

- `ELSE` is optional, the else values will be `NULL` without `ELSE`;
- Database checks the `WHEN` statements in order;
- We can use any [statement](#Comparison) used in `WHERE` in `CASE`;
- Useful application: use case statement to dealing with divide by zero;
- Can also be used under `WHERE`.

```sql
SELECT
	SUM (CASE WHEN hr=2 AND vehiclescash>400 THEN 1 ELSE 0 END) AS ct1
	, SUM (CASE WHEN hr=2 AND vehiclescash<5 THEN 1 ELSE 0 END) AS ct2
FROM
	cls.mta;

SELECT
	COUNT (CASE WHEN hr=2 AND vehiclescash>400 THEN 1 ELSE NULL END) AS ct1
	, COUNT (CASE WHEN hr=2 AND vehiclescash<5 THEN 1 ELSE NULL END) AS ct2
FROM
	cls.mta;
```

## `WHERE`

> Filtering out rows based on boolean logic.

```sql
SELECT
FROM
WHERE <comparison operation>;
```

* String is **case sensitive**;
* Using **single quote** for string;
* Using `AND` and `OR` to combine multiple criteria.

###Comparison

> used in `WHERE`

Common comparison operations: `=`, `>`, `<`, `<=`, `>=`, `!= or <>`.

`BETWEEN()`

```sql
<column> BETWEEN <number/string> AND <number/string>
```

- Inclusive: includes both end points
- String not recommend (p29)

`LIKE()` & `ILIKE()`

> match strings, search for specified patterns within a string

- `ILIKE()` is a case insensitive matching, `LIKE()` is case sensitive matching;
- `%`: matching any string;
- `_`: matching a single string;
- `_` requires a character to be there, however, `%` doesn't;

## `GROUP BY`

> combines similar values, aggregates, or collapses, data into a smaller number of rows.

- After `WHERE` clause;
- If `WHERE` clause removes a row, then that row will not be aggregated via the aggregation function;
- `GROUP BY` requires every column within the `SELECT` clause to be either inside a function or part of the `GROUP BY`;
- `NULL` will be treated as a single group if it is in the column being grouped;
- We can use `GROUP BY` statement on a `CASA` statement by column numbering in order to count(…) each categories.

### Aggregate Functions

`MAX`, `AVG`, `MIN`, `COUNT`, `SUM`

- Aggregate functions can be used without `GROUP BY` clause:

  - the entire table is treated as a single group within the `GROUP BY`;
  - every column within a `SELECT` statement is an aggregate function and it does not have `GROUP BY` put down.

- The database returns the column with the name of the aggregate function without `AS`;

- `COUNT` & `SUM`:

  | Syntax                 | return             |
  | ---------------------- | ------------------ |
  | SELECT COUNT(*)        | Number of rows     |
  | SELECT COUNT(1)        | Number of rows     |
  | SELECT 2 * COUNT(*)    | 2 * Number of rows |
  | SELECT 2 * COUNT(2)    | 2 * Number of rows |
  | SELECT 2 * COUNT(-1)   | 2 * Number of rows |
  | SELECT 2 * COUNT(NULL) | 0                  |
  | SELECT 2 * SUM(1)      | 2 * Number of rows |
  | SELECT 2 * SUM(2)      | 4 * Number of rows |

  - `COUNT(1)`: counting number of 1s appearing

- Aggregate functions all ignore `NULL` values;

- `COUNT(*)` is not ignore `NULL` values;

- If entire column is `NULL` within a group, then `AVG`, `MAX`, `MIN`, `SUM` will return `NULL` and `COUNT` will return 0;

- Aggregate function cannot be nested;

### Column Numbering

- the number in the `GROUP BY` clause denotes the number of column in the `SELECT` statement;
- we can add multiple columns.

### `HAVING`

> Working like a `WHERE` clause, but is evaluated after the `GROUP BY`.

- Can refer both to grouped expressions and to ungrouped expressions (which necessarily involve an aggregate function).

## `ORDER BY`

> Sorting returned data.

```sql
ORDER BY <column> ASC / DESC
```

* Default is ascending;

* `NULL` values are larger than non-nulls, when numbers; are alphabetically last;

* Sort character data in case insensitive manner;

* Multiple `ORDER BY` sorted sequentially;

  ```sql
  ORDER BY <column1> ASC / DESC, <column2> ASC /DESC
  ```

* Can order by columns that are not selected;

* When there is `DISTINCT` in `SELECT`, the column being sorted is the same one as the column being made distinct.

## `LIMIT`

> Limiting the number of rows returned.

```sql
LIMIT <number>
```

* Return arbitrary, rather than first;

* Not fully supported by alll version of SQL: (P19)

  | variant | syntax | example                                 |
  | ------- | ------ | --------------------------------------- |
  | MySQL   | LIMIT  | SELECT * FROM table LIMIT 10;           |
  | MS-SQL  | TOP    | SELECT TOP 10 * FROM table;             |
  | Oracle  | rownum | SELECT * FROM table WHERE rownum <= 10; |

* Combine `ORDER BY` and `LIMIT` to return the top X;

## `AS`

> rename columns / tables

- `AS` is not required;