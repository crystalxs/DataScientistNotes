# Group By

> combines similar values, aggregates, or collapses, data into a smaller number of rows.

* After `WHERE` clause;
* If `WHERE` clause removes a row, then that row will not be aggregated via the aggregation function;
* `GROUP BY` requires every column within the `SELECT` clause to be either inside a function or part of the `GROUP BY`;
* `NULL` will be treated as a single group if it is in the column being grouped;
* We can use `GROUP BY` statement on a `CASA` statement by column numbering in order to count(…) each categories.

## Aggregate Functions

`MAX`, `AVG`, `MIN`, `COUNT`, `SUM`

* Aggregate functions can be used without `GROUP BY` clause:

  * the entire table is treated as a single group within the `GROUP BY`;
  * every column within a `SELECT` statement is an aggregate function and it does not have `GROUP BY` put down.

* The database returns the column with the name of the aggregate function without `AS`;

* `COUNT` & `SUM`:

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

  * `COUNT(1)`: counting number of 1s appearing

* Aggregate functions all ignore `NULL` values;

* `COUNT(*)` is not ignore `NULL` values;

* If entire column is `NULL` within a group, then `AVG`, `MAX`, `MIN`, `SUM` will return `NULL` and `COUNT` will return 0;

* Aggregate function cannot be nested;

##Column Numbering

- the number in the `GROUP BY` clause denotes the number of column in the `SELECT` statement;
- we can add multiple columns.

## `HAVING`

> Working like a `WHERE` clause, but is evaluated after the `GROUP BY`.

