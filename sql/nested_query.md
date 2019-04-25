# Nested Query

## Subquery

**Uncorrelated**: nothing in the subquery references anything outside that subquery.

**Correlated**: references the outer query within the subquery.

`IN` & `NOT IN`

```SQL
WHERE <column> IN / NOT IN (<subquery>)
```

* Does not look at the name of the column within the subquery;
* 

`ANY` & `ALL`

```sql
WHERE <column> <OPERATOR> ANY / ALL (<subquery>)
```

## Joins

## Stacking

`UNION` & `UNION ALL`: stack tables vertically on each other.

```sql
SELECT <> FROM <>
UNION ALL
SELECT <> FROM <>
```

* Work on statements rather than tables;
* If the data from each column in the second table cannot be converted to the type in the upper table, the query will generate an error;
* `UNION` automatically deduplicate records;
* `UNION` is very expensive;

