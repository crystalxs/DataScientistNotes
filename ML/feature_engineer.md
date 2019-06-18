# Feature Engineering

> The process of formulating the most appropriate features given the goal, the algorithm, and the raw data.

## Common Approaches

### Learned models

Apply ML to Feature Engineering, typically unsupervised (e.g., dimension reduction or clustering).

In NLP, peform topic modeling (i.e., clustering) then classification within clusters

### Stacking

The outputs of one model become the inputs of another model

```python
Pipeline = [Transformer, Transformer, Transformer]
```

## Commom FE techniques

### Vectorizing

> **Categorical** (nominal or ordinal) needs to be transformed to a reasonable numbers for ML algorithms to be applied.

| Methods          | Size requirement                        | Growth                   |
| ---------------- | --------------------------------------- | ------------------------ |
| One-Hot Encoding | k # of categories                       | grow with new categories |
| Dummy Coding     | k-1 # of categories                     | grow with new categories |
| Feature Hashing  | m hash table size                       | fixed                    |
| Bin Counting     | m bin table size                        | fixed                    |
| Embedding        | d number of dimensions of feature space | fixed                    |

Tree based methods:

- When categorical feature is ordinal **label encoding** can lead to better quality if it preserves correct order of values. In this case a split made by a tree will divide the feature to values 'lower' and 'higher' that the value chosen for this split.

Non-tree based methods:

- One-hot encoding or embedings should be used.
- Unless there is a linear relashionship between the label encoding and the dependent variable non-tree based methods will have a hard time with label encoding.

#### One-Hot Encoding

> Takes each category value and turns it into a binary vector of size |i|(number of values in category i) where all columns are equal to zero besides the category column. 

- Often used for **linear models**.
- High cardinality can create very sparse data. One-hot-encoding can be used with sparse matrices.
- Produces very high dimensionality, this causes an increase in the model’s training and serving time and memory consumption.
- Can easily cause a model to overfit the data.
- Can’t handle categories that weren’t in the training data (e.g new city or device type). This can be problematic in domains that change all the time.
- Some of this disadvantages can be reduced by encoding all rare categories to the same features ("Other"). This method can reduce the dimensionality drastically in some datasets with a small or no decrease in performance.
- One-hot encoding a categorical feature with huge number of values can lead to high memory consumption. You can use sparse matrices to deal with this problem.

#### Label encoding

> Encode labels with value between 0 and n_classes-1.

- It is used to transform non-numerical labels to numerical labels.
- This method is usedful for **tree-based** methods.

#### Frequency encoding

> Each category is replaced by the frequency of that category in the training data.

- Used for tree-based methods.

#### Target or mean encoding

> Use the target variable to generate features.

- Note that mean encodoing needs to be computed on train and joined latter with validation and test.

```python
data = pd.DataFrame({
        'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'],
        'y': [1, 1, 0, 0, 0]})
m =  pd.DataFrame({'y_mean' : data["y"].groupby(data["state"]).mean()}).reset_index()
pd.merge(data, m, how="left", on=["state"])
```

#### Feature Hashing

> Fit a model on the hash indexes as features. The raw data is vectorized and compressed but loses all interpretability.

Hashes the high dimensional input vectors $x \in R^n$ into a lower dimensional feature space $R^m$ where $m << n$. The hashing-trick preserves sparsity and approximately preserves the Euclidean norm.

It is often use for representing text but it can also be used for in settings with a large number of categories.

Pros:

- It is low dimensional thus it is very efficient in processing time and memory.
- It can be computed online (without seeing all the data)

Cons:

- Hashing functions sometimes have collision so if H(New York) = H(Tehran) the model can’t know what city were in the data. Studies have shown that collisions usually doesn’t affect significantly on the models performance.
- Hashed features are not interpretable so doing things like feature importance and model debugging is very hard.

#### Bin Counting

> Rather than using the value of the categorical variable as the feature, instead use the **conditional probability of the target under that value**.

Turns a large, sparse, binary representation of the categorical variable (e.g., one-hot encoding) into a very small, dense, real-valued numeric representation.

#### Embeddings

> https://blog.myyellowroad.com/using-categorical-data-in-machine-learning-with-python-from-dummy-variables-to-deep-category-42fd0a43b009

If you have any sequential discrete data, embedded it. Examples: Words, emojis, website browsing, images, videos, product purchasing

### Binning, aka Quantization

> Discretize **continuous** values into a smaller number of "bins".

* It makes sense for your goal (e.g., categorize people's age by decade for marketing)
* Improve signal-to-noise ratio (e.g., aggregate GPS data)
* Fitting a model to bins reduces the impact that small fluctuates in the data has on the model, often small fluctuates are just noise. Each bin "smooths" out the fluctuates/noises in sections of the data.

### Transforming

#### Linear

- Most commonly each data value is added or multiplied by the same constant
- **Example**: Normalization & Standardization
- Generally fine
- Linear preserves the operations of addition and scalar multiplication

##### Normalization vs standardization

|               | Normalization (min-max scaling)               | Standardization                      |
| ------------- | --------------------------------------------- | ------------------------------------ |
| Function      | $x = \frac{x-min(x)}{max(x)-min(x)}$          | $x_{changed} = \frac{x-\mu}{\sigma}$ |
| Rescale Range | [0,1]                                         | $[-\infty, \infty]$                  |
| Outliers      | Outliers from the data set are **compressed** | **Retains** outlier values           |

#### Nonlinear

- Mostly commonly each data value is added or multiplied by a different value
- **Examples**: Squaring each value
- "With great power, comes great responsibility"
- Nonlinear does **NOT** preserves the operations of addition and scalar multiplication

#### Rescaling

Often features are orders of magnitude different from each other.

Several ML algorithms are sensitive to feature scaling, they exploit distances or similarities between data samples:

- K-NN
- SVM
- neural network

### Special Type of Data

#### Date and time

- Periodicity
  - Day number in week, month, season, year, second, minute, hour.
- Time since
- Difference between dates

#### Coordinates

- Distance to interesting points from external data or training data
- Cluster your data and use the center of the cluster to compute distances
- Compute agregated statistics
  - Mean sale price per neighborhood

#### Aggregate by one or multiple categorical features

> Using `groupby` to aggregate to a new dataframe and then use `merge` to make the new feature.

Here are some fetures that we can compute

- Number of times `device_ip` appears on the training data. It would be better if we had `user_id`.
- Number of times `device_ip` appears per month on the training data.
- Min, max, average `C1` per `site_id`.

#### Features based on KNN

K nearest neighbor (KNN) classifier. Looks at the K points in the training set that are nearest to the test input xx and returns the mean of the target variable.

### Feature selection

> Way to remove uninformative features.

#### Methods

1. Check correlation
2. Filtering
3. Wrapper methods
4. Embedded methods
5. sklearn `feature_selection`
6. deep learning