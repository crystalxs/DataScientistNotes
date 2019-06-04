# Query Notes

## Scope (P7)

## Evaluation Order

1. `FROM`
2. `WHERE`
3. `GROUP BY` + `HAVING`
4. `SELECT` + Window Function
5. `ORDER BY`
6. `LIMIT`
7. 

## Case Sensitive v.s. Case Insensitive

### Case Sensitive

* In string itself, such as `WHERE vehicle type = 'Semi Trailer'`;

### Case Insensitive

* Alphabetical order

## Quotes

* **Double quotes**: used to refer to database object ( tables, columns and schemas);
* **Single quotes**: 

## Column Numbering

> Use number to refer the column position in `SELECT`.

**ALLOWANCE**

* `ORDER BY`
* `GROUP BY`

## Costly Computationally

* Correlated subquery
* `DISTINCT`
* `UNION`
* 