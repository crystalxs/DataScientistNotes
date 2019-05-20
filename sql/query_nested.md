# Nested Query

## Subquery

* Use `DISTINCT` in the subquery itself.

**Uncorrelated**: nothing in the subquery references anything outside that subquery.

**Correlated**: references the outer query within the subquery.

`IN` & `NOT IN`

```SQL
WHERE <column> IN / NOT IN (<subquery>)
```

- Does not look at the name of the column within the subquery;
- Can be used without a `SELECT`: `WHERE <column> IN (1, 2);`

`ANY` & `ALL`

```sql
WHERE <column> <OPERATOR> ANY / ALL (<subquery>)
```

## Joins

> Combining tables side-by-side.

- Always have a unique side;
- Labeling each of the tables that you are joining on based either on:
  - location or position ('LHS', 'RHS');
  - contents or data they contain
- Joins order:
  - Inner
  - Left
  - Outer
  - Cross
- Consistent with `USING`/`ON`/`WHERE`:
  - `WHERE`: filtering conditions;
  - `ON`: matching;
  - `USING`: only when it makes sense.

### `ON`

> Defining which column matches.

Any boolean condition or set of conditions can be put in here by using parenthesis, `AND` and `OR`.

### `USING`

> If the columns that matching on have the same name.

- Only output one column of the matching columns;
- Can be used with multiple columns (separate them with comma);
- Create a synthetic column using a similar construct as the `COALESCE` statement.

### `LEFT JOIN`

> Keeping all records from the first table (the "Left Hand Side") and only those records that match from the second table (the "Right Hand Side").

### `RIGHT JOIN`

> Keeping all records from the second table (the "Right Hand Side") and only those records that match from the first table (the "Left Hand Side").

### `INNER JOIN` (`JOIN`)

> Keeping rows that are in both tables.

### `FULL JOIN` (`OUTER JOIN` / `FULL OUTER JOIN`)

> Keeping all rows from either table.

### `CROSS JOIN`

> Creating every possible combination of rows.

- No need `ON`;
- Can be useful when looking for missing data or trying to fill-in data;

## `UNION` & `UNION ALL`

> Stacking tables vertically on each other - appending the data.

```sql
SELECT <> FROM <>
UNION (ALL)
SELECT <> FROM <>
```

- Work on statements rather than tables;
- If the data from each column in the second table cannot be converted to the type in the upper table, the query will generate an error;
- `UNION` automatically deduplicate records;
- `UNION` is very expensive;

