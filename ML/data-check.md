# Check Data

## First Look

### Check Data Type and Memory Usage

> `df.info(memory_usage=deep)`
>
> `df.head()`

| memory usage | float   | int   | uint   | datetime   | bool | object |
| :----------- | :------ | :---- | :----- | :--------- | :--- | :----- |
| 1 bytes      |         | int8  | uint8  |            | bool |        |
| 2 bytes      | float16 | int16 | uint16 |            |      |        |
| 4 bytes      | float32 | int32 | uint32 |            |      |        |
| 8 bytes      | float64 | int64 | uint64 | datetime64 |      |        |
| variable     |         |       |        |            |      | object |

#### Before loading data

> Use `dtype` to specific the data type and to reduce the memory usage.

```python
types = {'id': np.uint32, 'click': np.uint8, 'hour': np.uint32, 'C1': np.uint32, 'banner_pos': np.uint32,
         'site_id': 'category', 'site_domain': 'category', 'site_category': 'category', 'app_id': 'category',
         'app_domain': 'category', 'app_category': 'category', 'device_id': 'category',
         'device_ip': 'category', 'device_model': 'category', 'device_type': np.uint8, 'device_conn_type': np.uint8,
         'C14': np.uint16, 'C15': np.uint16, 'C16': np.uint16, 'C17': np.uint16, 'C18': np.uint16, 'C19': np.uint16,
         'C20': np.uint16, 'C21': np.uint16}

data = pd.read_csv(path + "train", usecols=types.keys(), dtype=types)
print(data.info(memory_usage='deep'))
```

#### After loading data

##### Numerical

> Use the function `pd.to_numeric()` to **downcast** our numeric types. We’ll use `DataFrame.select_dtypes` to select only the integer columns, then we’ll optimize the types and compare the memory usage.

```python
data_int = data.select_dtypes(include=['int'])
converted_int = data_int.apply(pd.to_numeric,downcast='unsigned')
```

##### Object

> The `category` type uses integer values under the hood to represent the values in a column, rather than the raw values. Pandas uses a separate mapping dictionary that maps the integer values to the raw ones. This arrangement is useful whenever a column contains a limited set of values. When we convert a column to the `category` dtype, pandas uses the most space efficient `int` subtype that can represent all of the unique values in a column.

```python
dow_cat = data['col'].astype('category')
# use the Series.cat.codes attribute to return the integer values the category type uses to represent each value.
dow_cat.head().cat.codes
```

* If this column has any missing values, the `category` subtype handles missing values by setting them to `-1`.
* Be aware of the trade-offs. The biggest one is the inability to perform numerical computations. We can’t do arithmetic with `category` columns or use methods like `Series.min()` and `Series.max()` without converting to a true numeric dtype first.
* We should stick to using the `category` type primarily for `object` columns where less than 50% of the values are unique. If all of the values in a column are unique, the `category` type will end up using *more* memory. That’s because the column is storing all of the raw string values in addition to the integer category codes.

##### Datetime

* You may remember that this was read in as an integer type and already optimized to `unint32`. Because of this, converting it to `datetime` will actually double it’s memory usage, as the `datetime` type is a 64 bit type.
* There’s value in converting it to `datetime` anyway since it will allow us to more easily do time series analysis.

```python
optimized_gl['date'] = pd.to_datetime(date,format='%Y%m%d')
```

### Check Duplicate

> `data.drop_duplicates()`

## Numerical Features - Check Distribution

`df.describe()`: statistics check, look at min and max of every column.

`np.quantile(X, [0.1, 0.5, 0.95, 1], axis=0, keepdims=True)`

`plt.hist(X[:,0], bins='auto')`

### Check Correlation

> perfect multi-correlation > 90%

* Remove the highly correlated variable to save time for feature engineering.

### Feature scaling

> Linear models, neural networks and KNN need **feature scaling** while tree-based methods don't need scaling.

- KNN needs feature scaling because the distance between points is greatly afected by scaling.
- Linear models and Neural Nets need scaling
  - The amount of regularization applied to a feature depends on the feature's scale.
  - Optimization methods converge more rapidly when features are scaled.
- Scales are computed on the training set and applied to the test/validation sets.
- Need to deal with outliers.

#### MinMaxScaler (normalization)

- Transforms features by scaling each feature to a given range.
- Preserves relative distances between measurements.
- It is very sensitive to the presence of **outliers**.

```python
min = X.min() 
max = X.max() 
X = (X - min)/(max - min)
```

#### Standard Scaler (standardization)

This has the virtue of preserving relative distances between measurements. The outliers have an influence when computing the empirical mean and standard deviation.

```python
mean = X.mean()
std = X.std()
X = (X - mean)/std
```

#### Clip Outliers

There are valid reasons for throwing away outliers. For example, a measurement resulting from a human error. In general throwing away observations is a questionable practice.

**Summary**: if we see outliers that don't make sense you can discard observations with > 99% quantile or <1% quantile. Or you can "clip" by changing the values to the 99% quantile or 1% quantile. Here is an example.

```pythono
{92, 19, 101, 58, 1053, 91, 26, 78, 10, 13, -40, 101, 86, 85, 15, 89, 89, 28, -5, 41} 
to
{92, 19, 101, 58, 101, 91, 26, 78, 10, 13, -5, 101, 86, 85, 15, 89, 89, 28, -5, 41}
```

#### Rank transformation

Example: rank([-100, 0, 10000]) = [1,2,3]

- It smooths out unusual distributions and is less influenced by outliers than scaling methods.
- It distort correlations and distances within and across features.
- Provides non-linear transformations in which distances between marginal outliers and inliers are shrunk.

```python
scipy.stats.rankdata([-100,-100,0,100000])
# array([1.5, 1.5, 3. , 4. ])
```

#### Power transformations

A common way of analyzing data that is not normally distributed is to transform it so that it become closer to normal. In particular, if your data is right-skewed you can use log or square root.

```python
np.log(x + 1)
np.sqrt(x + 1)
```

## Categorical and Ordinal Features

> Ordinal = Ordered categorical features.
>
> `df['col'].value_counts()`

* Label encoding can be used by tree-based method. 
* For non tree-based method use one-hot-encoding (or embeddings which will be discussed later)
* High cardinality can create very sparse data. One-hot-encoding can be used with sparse matrices.
* Difficult to impute missing values. NA can be treated as another category.

### Label encoding

> Encode labels with value between 0 and n_classes-1.

* It is used to transform non-numerical labels to numerical labels.
* This method is usedful for **tree-based** methods.

### One-hot encoding

> 

- Often used for linear models
- Produces very high dimensionality, this causes an increase in the model’s training and serving time and memory consumption.
- Can easily cause a model to overfit the data.
- Can’t handle categories that weren’t in the training data (e.g new city or device type). This can be problematic in domains that change all the time.
- Some of this disadvantages can be reduced by encoding all rare categories to the same features ("Other"). This method can reduce the dimensionality drastically in some datasets with a small or no decrease in performance.
- One-hot encoding a categorical feature with huge number of values can lead to high memory consumption. You can use sparse matrices to deal with this problem.

#### Label encoding v.s. one-hot encoding

> When to use label encoding versus one-hot encoding.

Tree based methods:

- When categorical feature is ordinal **label encoding** can lead to better quality if it preserves correct order of values. In this case a split made by a tree will divide the feature to values 'lower' and 'higher' that the value chosen for this split.

Non-tree based methods:

- One-hot encoding or embedings should be used.
- Unless there is a linear relashionship between the label encoding and the dependent variable non-tree based methods will have a hard time with label encoding.

### Frequency encoding

> Each category is replaced by the frequency of that category in the training data.

* Used for tree-based methods.

### Target or mean encoding

> Use the target variable to generate features.

* Note that mean encodoing needs to be computed on train and joined latter with validation and test.

```python
data = pd.DataFrame({
        'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'],
        'y': [1, 1, 0, 0, 0]})
m =  pd.DataFrame({'y_mean' : data["y"].groupby(data["state"]).mean()}).reset_index()
pd.merge(data, m, how="left", on=["state"])
```

### Feature hashing (hashing trick)

Hashes the high dimensional input vectors $x \in R^n$ into a lower dimensional feature space $R^m$ where $m << n$. The hashing-trick preserves sparsity and approximately preserves the Euclidean norm.

It is often use for representing text but it can also be used for in settings with a large number of categories.

Pros:

- It is low dimensional thus it is very efficient in processing time and memory.
- It can be computed online (without seeing all the data)

Cons:

- Hashing functions sometimes have collision so if H(New York) = H(Tehran) the model can’t know what city were in the data. Studies have shown that collisions usually doesn’t affect significantly on the models performance.
- Hashed features are not interpretable so doing things like feature importance and model debugging is very hard.

