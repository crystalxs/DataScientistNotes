# Pandas

> <http://pandas.pydata.org/pandas-docs/stable/>

```bash
conda install pandas
pip install pandas
```

```python
import pandas as pd
```

## Load data

> <http://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv>

```python
df = pd.Series(<list>)						# 1 dimension
df = pd.DataFrame(<dictionary>)	# 2 dimension
# example
df = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series(1, index=list(range(4)), dtype='float32'),
                    'D': np.array([3] * 4, dtype='int32'),
                    'E': pd.Categorical(["test", "train", "test", "train"]),
                    'F': 'foo'})
df = pd.read_csv(<filepath>)
df = pd.read_feather(<filepath>)
```

##### Useful options

`sep=','` (`delimiter=','`): delimiter to use;

`header=<num>`: row number(s) to use as the column names (<num> means first line of data);

`header=None`: row names are passed explicitly;

## Overview data

```python
df.info()
```

## Data type

> <http://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#dtypes>

Pandas uses NumPy arrays and dtypes for Series or individual columns of a DataFrame. 

* `float`, `int`, `bool`, `timedelta64[ns]` and `datetime64[ns]` (note that NumPy does not support timezone-aware datetimes);
* `object` (for string), `Timestamp`, `Categorical`, `Intervals`;
* etc

### Check type

```python
df.dtypes		# give dtype for each column
series.dtype
```

### Convert type

```python
df.<column> = df.<column>.astype(<data type>)
df = df.astype({<col1>:<type>, <col2>:<type>})

pd.to_numeric(df.<column>)
pd.to_datetime(df.<column>)
pd.to_timedelta(df.<column>)
df.<column>.map(<dictionary>)
```

### String function

```python
# <column> is str type
df.<column>.str.lower()		# normalize to lower case
df.<column>.str.upper()
df.<column>.str.len()
df.<column>.str.strip()		# lsrtip rstrip
df.<column>.str.replace()
df.<column>.str.split()
sf.<column>.str.contains(<string>)
df.<column>.str.cat()			# concatenate a series into string
```

### dates function

```python
# <column> is date type
df.<column>.dt.dayofweek
df.<column>.dt.day
df.<column>.dt.month
```

## Access data

###Get column

> df.columns	# give columns' name

```sql
df.<column>
df['<column>']
df[['<column1>', '<column2>']]
df.iloc[:,<column num>]
df.loc[:,<column>]
df.<column>.values
```

### Get row

```python
df.head(<num>)
df.tile(<num>)
df.nlargest(<num>, <column>)
df.nsmallest(<num>, <column>)

# by position
df.iloc[<index num>]
df.iloc[<index num>,:]
df.iloc[<start row num>:<end row num+1>]

# by label
df.loc[<value>]		# based on index value
df.loc[<value>,:]

# Slice data

df[<start position>:<end position + 1>:<step>]
# If <step> is negative, the <start position> is in the end.
```

####Index

```sql
df.reset_index()
df.set_index('<column>')
df.sort_index()
```

### Get data based on condition (boolean indexing)

```python
df[<condition>]

# <condition> example
df.<column>.isin(<list>)
df.<column>.any()
df.<column>.all()
df.<column>.empty					# check whether the column is empty

df.where()
df.mask()									# inverse of .where()
```

####Condition operation

| Operator | description           |
| -------- | --------------------- |
| <        | less than             |
| >        | greater than          |
| ==       | equal                 |
| !=       | not equal             |
| <=       | less than or equal    |
| >=       | greater than or equal |

#### Logic operation

| Operator | description |
| -------- | ----------- |
| &        | and         |
| \|       | or          |
| ~        | not         |

These **must** be grouped by using parentheses.

### Iteration

Basic iteration (`for i in object`) produces:

- **Series**: values
- **DataFrame**: column labels
- **Panel**: item labels

`iterrows()`: iterate over the rows of a DataFrame as (index, Series) pairs;

`itertuples()`: iterate over the rows of a DataFrame as namedtuples of the values;

`iteritems()` iterates through key-value pairs:

- **Series**: (index, scalar value) pairs
- **DataFrame**: (column, Series) pairs
- **Panel**: (item, DataFrame) pairs

## Check data

###Summary

```python
df.describe()
df.<column>.sort_values(ascending=False)
df.sort_values('<column>', ascending=False)
df.<column>.value_counts()		# count num of rows with unique values
df.<column>.nunique()
.sum()
.count()
.median()
.quantile([0.25, 0.75])
.min()
.max()
.mean()
.var()
.std()
.mode()
.abs()
.cumsum()
.cummax()
.cummin()
```

All such methods have a `skipna` option signaling whether to exclude missing data (`True` by default).

### Null

```python
df.isnull()		# matrix
df.notnull()
df.isnull().any()		# column wise
df.<column>.isnull	# row wise under that column
```

### Missing values

> pandas primarily uses the value `np.nan` to represent missing data.

```python
pd.isna(df)		# find missing value
df.dropna()		# drop rows where have missing value
df.fillna(<value>)		# fill missing value
```

### ???

```python
df.drop_duplicates()
df.rename(columns={<column>: <new column>})
```

##Group

```python
df.groupby()
```

## Merge

```python
pd.concat([<df1>, <df2>])					# row wise
pd.concat([<df1>, <df2>], axis=1)	# column wise
df.append()
pd.merge(<left df>, <right df>, on='<key>')
```

###Reshape

```python
df.stack()
df.unstack()
pd.pivot_table(df,)
```



## Save data

```python
df.to_feather(<filepath>)		# feather format

```



## Delete data

```python
df.drop(columns=['<column>'])		# drop column
del df
```

