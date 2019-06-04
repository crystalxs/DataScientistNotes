# View

> Storing query masquerading as a table.

- Could be easily access using SQL;
- It will be in the `information_schema`;

###Create

```sql
	CREATE VIEW <schema>.<view> AS
	<query>;
```

###Drop

```sql
DROP VIEW <schema>.<view>;
```

###Advantage

* Shared query
* Version control
* Laziness

###Disadvantage

* Performance considerations
* Proliferation of views

## `WITH`

> Allow for tables to be defined and used repeatedly within a query.

```sql
WITH <name> as (<query>)
SELECT * FROM <name>;
```

* No comma between `WITH` and `SELECT` statement;

### Advantage

- Easier to read
- Laziness

### Disadvantage

- Some database do not support them
- Can act as optimization barriers