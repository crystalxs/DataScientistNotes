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

## Check Balanced

###Unbalance on Target

#### Ignore it

It might not matter (seriously).

Small-ish differences at large scale might not effect business outcomes.

#### Resampling

1. Over sample minority group, eg SMOTE
2. Under sample majority group
3. Representative sampling of both groups (stratify)

#### Evaluation Metrics

Avoid accuracy. Use F-score and AUC.

#### Robust algorithm

eg. SVM is very robust to class Imbalances.

#### Loss function

Weight mistakes for smaller classes more highly than mistakes for larger classes.

##### What is the difference between error and loss?

**Error** is a mistake.

**Loss** is a **weighted** mistake.

### Unbalanced on Features

If we want to split on a feature, it would be best if both features are relatively balanced.

### Unbalanced on Regression

In Regression, we want to predict a value. It is best if all possible values are equally represented.

## Check Missing Value

> Be very careful that the missing data is not systematic of the effect you are studying. Maybe missing data could be a feature (not a bug).

- Treat categories present in the test data but not present in the train data as missing values.
- Some methods like XGBoost can handle missing values.

### Keep it

* Missing values can be hidden from `isna` (replaced by 9999).
* Add a new column `is_null` for every feature with missing values.

### Drop it

* Drop rows (instances)
* Drop columns (features)

### Impute values

- Go get the missing data
- Sample from existing values
- Deep Learning
- Replacing missing values
  - mean/medium of existing values for continue variable
  - recent/majority of existing values for category variable
  - -999 works for tree-based methods
  - reconstruct mission value (train a model on other features to estimate missing value)
    - Regression is often used because it is multivariate mean estimation
    - k-NN works well

## Numerical Features

`df.describe()`: statistics check, look at min and max of every column.

`np.quantile(X, [0.1, 0.5, 0.95, 1], axis=0, keepdims=True)`

`plt.hist(X[:,0], bins='auto')`

### Check Correlation

> perfect multi-correlation > 90%

* Remove the highly correlated variable to save time for feature engineering.

### Check Distribution - Feature scaling

> Linear models, neural networks and KNN need **feature scaling** while tree-based methods don't need scaling.
>
> https://scikit-learn.org/stable/auto_examples/preprocessing/plot_all_scaling.html

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

### Deal with Outlier

> https://www.theanalysisfactor.com/outliers-to-drop-or-not-to-drop/

**Outliers v.s. Anomaly Detection**

**Outliers:** generated by the **same** statistical process as your data (just unusual spread).

**Anomaly:** generated by a **different** statistical process as your data.

#### Remove

> There are valid reasons for throwing away outliers. For example, a measurement resulting from a human error. In general throwing away observations is a questionable practice.

#### Clip Outliers

> If we see outliers that don't make sense you can discard observations with > 99% quantile or <1% quantile. Or you can "clip" by changing the values to the 99% quantile or 1% quantile. Here is an example.

* Prevent out-of-bound values (mostly for unreasonable x)

```pythono
{92, 19, 101, 58, 1053, 91, 26, 78, 10, 13, -40, 101, 86, 85, 15, 89, 89, 28, -5, 41} 
to
{92, 19, 101, 58, 101, 91, 26, 78, 10, 13, -5, 101, 86, 85, 15, 89, 89, 28, -5, 41}
```

#### Log box-cox (param)

#### Cost function

* Use MAE as cost function.

## Categorical and Ordinal Features

> Ordinal = Ordered categorical features.
>
> `df['col'].value_counts()`

* High cardinality can create very sparse data. One-hot-encoding can be used with sparse matrices.
* Difficult to impute missing values. NA can be treated as another category.
* Label encoding can be used by tree-based method. 
* For non tree-based method use one-hot-encoding (or embeddings which will be discussed later)