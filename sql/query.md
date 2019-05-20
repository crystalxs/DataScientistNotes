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

Common comparison operations: `=`, `>`, `<`, `<=`, `>=`, `!= / <>`.

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

## `CASE`

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

* `ELSE` is optional, the else values will be `NULL` without `ELSE`;
* Database checks the `WHEN` statements in order;
* We can use any [statement](#Comparison) used in `WHERE` in `CASE`;
* Useful application: use case statement to dealing with divide by zero;
* 

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

## `AS`

> rename columns / tables

- `AS` is not required;

## `DISTINCT`

> Removing duplicates from the data that is being returned.

* `DISTINCT` is computationally expensive;
* Common error occurred when sort: `DISTINCT` and `ORDER BY` can be used only when the column being sorted is the same one as the column being made distinct.

## `COALESCE`

> Return the first non-Null value it encounters.

If  all values are `NULL`, then a `NULL` is returned.

