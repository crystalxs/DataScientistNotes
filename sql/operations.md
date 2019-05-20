# Operations

> CRUD (P23)

##Create:

### `CREATE`

> Creating a container for data to be stored.

```sql
CREATE TABLE <schema>.<table> (
  <column1> <type>
  , <column2> <type>
);
```

### `INSERT`

> Putting data into a container.

```sql
INSERT INTO <schema>.<table> VALUES (<column1 value>, <column2 value>), (<column1 value>, <column2 value>), (<column1 value>, <column2 value>);
```

### `COPY`

> Bulking data loading into a container.

## Read - [`SELECT`](query.md)

##Update

### `UPDATE`

> Changing the **data** in the table.

```sql
UPDATE <schema>.<table> SET <column> = <functions> (WHERE <condition>);
```

### `ALTER`

> Changing the structure of a **table**.

##Delete

### `DROP`

> Removing **database object**.

### `DELETE`

> Removing **data** from table.

```sql
DELETE FROM <schema>.<table> (WHERE <condition>);
```

## `UPSERT`

> Portmanteau of `UPDATE` and `INSERT`, will insert a new row unless that row is already present, in which case it will update.