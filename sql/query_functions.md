# Functions

## Common Functions

> Generally operate on a single row of data

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

- Default is to remove space;
- `LTRIM()` & `RTRIM()`: trim from only a single side

`||`: put two strings together	

| VARIANT    | SYNTAX     |
| ---------- | ---------- |
| MySQL      | `CONCAT()` |
| MS-SQL     | `+`        |
| PostgreSQL | `||`       |

## Analytic Functions (Window Functions)

```sql
<function> () over (
  (PARTITION BY ***)
  (ORDER BY)
  <window frame clause>
)
```

* <function>:

  * can be one of any of standard aggregate functions: `SUM`, `COUNT`, `MAX`, `MIN`, `AVG`;
  * `ROW_NUMBER()`: return the row number based on the criteria;
  * `LAG()` and `LEAD()`: return the value of a column from a preceding or following row;
  * `FIRST_VALUE()` and `LAST_VALUE()`: return the first and last value within a partition;
  * `NTILE()`: handles percentiles;

* `OVER()`: tells database to expect a window function over entire table;

* `PARTITION BY`: tells database how to break up the data, similar to a `GROUP BY`;

* `ORDER BY`: tells database how to sort the data **within each partition**, works as an `ORDER BY` in normal;

  * when present, the function is calculated in a running fashion, from the start of the partition to the current row, **plus any following rows that are equal to the current row**;
  * when omit, the default frame consists of all rows in the partition;

* <window frame clause>: defines the region over which the function is calculated:

  ```sql
  ROWS BETWEEN **** AND ****
  ```

  * `UNBOUNDED PRECEDING`
  * `UNBOUNDED FOLLOWING`
  * `** PRECEDING`
  * `** FOLLOWING`
  * `CURRENT ROW`
  * this function is inclusive;
  * the row order returned is arbitrary if without `ORDER BY`;
  * 

  

