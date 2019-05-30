# Spark SQL

> Working with `DataFrame`

## Initiate SparkSession

The entry point to programming Spark with the DataFrame API.

```python
from pyspark.sql import SparkSession
ss = SparkSession.builder.getOrCreate()
```

## DataFrame

Handle structured, distributed data with a table-like representation with named column declared with column types.

### Check DataFrame

**`.printSchema()`.**: checking the schema.

**`.show(num_rows)`.**: checking the DataFrame.

### Creating DataFrame

> Spark SQL lets you register DataFrames from different sources (SQL, Parquet, JSON, ORC), Pandas dataframe as tables in the table catalog and query them. 

#### RDDs.

`.toDF()`: using RDDs containing row data as tuples.

- `.toDF()`.
- `.toDF(columnnames)`, where `columnnames = ['column1', 'column2', ...]`.

**Limitation:**

- All the columns are string type.
- All the columns are nullable.

`.createDataFrame(data, schema=None, samplingRatio=None, verifySchema=True)`: specifying a schema.

- `data`: an RDD of row/tuple/list/dict, list or pandas.DataFrame.
- `schema`: a StructType or list of column names.
  - `schema = StructType([StructField("colomn1", DataType, True/False), ...])`
  - `StructType`: Representing rows. Consisting of a list of StructField.
  - `StructField`: Representing columns. Including column name(string), data type, nullable(default: True), metadata(default: None). 
    - Need to add `from pyspark.sql.types import *`
    - DataType: `NullType()`, `StringType()`, `BinaryType()`, `BooleanType()`, `DateType()`, `TimstampType()`,
      `DoubleType()`, `FloatType()`, `IntegerType()`, `ArrayType()` etc.
- `samplingRatio`: the sample ratio of rows used for inferring the schema.
- `verifySchema`: verify data types of every row against schema. 

**Fix error**: in case there are non-integer type to be converted.

```python
def IntegerSafe(value):
    try:
        return int(value)
    except ValueError:
        return None
```

#### File

- JSON: `ss.read.json(<file_name>, schema, etc)`.
- CSV: `ss.read.csv(<file_name>, schema, etc)`.

#### Database

> Relational database and other DB with JDBC

##### Relational DB

* Download a Postgres JDBC jar from https://jdbc.postgresql.org/download.html

* `pyspark --driver-class-path Postgres_JDBC_location`

  ```python
  from pyspark.sql import DataFrameReader
  df = DataFrameReader(sqlContext).jdbc(url='jdbc:<URL>', table='<table_name>', properties=<property_list>), where <property_list> includes user, password and driver.
  ```

##### MongoDB

- Provide the `mongo-spark-connector` package as a packages parameter value:

- ```python
  import os
  pyspark_submit_args = '--packages org.mongodb.spark:mongo-spark-connector_2.11:2.4.0 pyspark-shell'
  os.environ["PYSPARK_SUBMIT_ARGS"] = pyspark_submit_args
  ```

- Provide `spark.mongodb.input.uri` and its URI, DB and collection:

- ```python
  spark = SparkSession \
      .builder \
      .appName("ex14") \
      .config("spark.mongodb.input.uri", "mongodb://127.0.0.1/msds694.business")\
      .getOrCreate()
  ```

- `ss.read.format("com.mongodb.spark.sql.DefaultSource").load()`

#### Middle RDD data

`df = spark.createDataFrame(pickleRdd)`

### Registering DataFrame in the Table Catalog

- You can reference a DataFrame by its name by registering the DataFrame as a table.
- Spark stores the table definition in the table catalog.
- Save as table: `.write.saveAsTable(<table_name>)`
  - Register a table permanently.
  - The table definitions will survive your application’s restarts and are persistent 
- Once DataFrame is registered as a table, you can query its data using SQL expressions.
  - **`ss.sql(sql_query)`**

### Convert to RDD

`.rdd()`

### DateFrame API

> https://spark.apache.org/docs/2.3.0/api/python/pyspark.sql.html

- `select(<column names>/list of dataframe[<column_name>])`
- `drop(<column names>)`: **select all except the given columns.**
- `filter(<constraints>)`
- `where(<constraints>)`
- `withColumnRenamed(<existing_col_name>, <new_col_name>)`: rename columns.
- `withColumn(<column_name>, <column_expression>)`: add columns.
- `orderBy(<column>, ascending = True)`
- `sort(<column>, ascending = True)`
- `alias(<column_name>)`: name columns.

## SQL functions

### Scalar functions

> Return a single value for each row based on calculations on one or more columns. 

- Math: `abs`, `log`, `avg`, `count`, etc.
- String: `length`, `concat`, `trim`, `contains`, etc.
- Time: `year`, `date_add`, `datediff`, `next_day`, etc.

### Aggregate functions

> Return a single value for a group of rows.

Can be used in combination with `groupBy()`.

- `df.groupBy().agg(<column_name>)`

`df.select(avg(df.<column_name>))`

### Window functions

> Return several values for a group of rows. 

| Sql          | dataframe api                       | description |
| ------------ | ----------------------------------- | ----------- |
| rank         | rank                                |             |
| dense_rank   | denseRank                           |             |
| percent_rank | percentRank                         |             |
| ntile        | ntile(<n>)                          |             |
| row_number   | rowNumber                           |             |
| cume_dist    | cumeDist                            |             |
| first_value  | firstValue                          |             |
| last_value   | lastValue                           |             |
| lag          | lag(<column>, <offset>, [default])  |             |
| lead         | lead(<column>, <offset>, [default]) |             |

1. Construct a column definition with an aggregate function or window functions. 

2. Build a window specification and use it as an argument to `over()` function. 
   1. Define the partition using `partitionBy()` function. 
   2. Specify ordering in the partition using `orderBy()`. 

### User-defined functions

> Generate custom scalar or aggregate functions. 

```python
from pyspark.sql.functions import *

udf_name = udf(lambda function definition)
data_frame.select(udf_name(col))
```

### Grouping Data

`.groupBy()`

- Take column names or a list of column objects.
- Return GroupedData Object.
- `.groupBy(col).max(col)`
- `.groupBy(col).agg(max(col), min(col),...)`

### Joining Data

`df1.join(df2, condition or column name, join_type)`

- `join_type`:
  - `inner`(default)
  - `left_outer`
  - `right_outer`
  - `outer`: return unmatched rows from both tables.
  - `leftsemi`: get the names within left table that appear in right table, only contain the columns in left table, don't include the columns in right table.