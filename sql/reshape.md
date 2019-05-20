# Reshape Data

## Long to Wide

```sql
SELECT <column>
	, MAX(CASE WHEN <condition> THEN ** ELSE ** END) AS <column>
  , MAX(CASE WHEN <condition> THEN ** ELSE ** END) AS <column>
FROM <table>
GROUP BY 1;
```

## Wide to Long

```sql
SELECT <column>
	, CASE
			WHEN <condition> THEN **
			WHEN <condition> THEN **
			ELSE ** END AS <column>
FROM <table>;
```

