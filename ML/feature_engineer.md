# Feature Engineering

> The process of formulating the most appropriate features given the goal, the algorithm, and the raw data.

## Common Approaches

### Hand crafted rules

* A good place to start
* Very common
* Requires domain expertise

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

#### One-Hot Encoding

#### Dummy Coding

#### Feature Hashing

> Fit a model on the hash indexes as features. The raw data is vectorized and compressed but loses all interpretability.

#### Bin Counting

> Rather than using the value of the categorical variable as the feature, instead use the **conditional probability of the target under that value**.

Turns a large, sparse, binary representation of the categorical variable (e.g., one-hot encoding) into a very small, dense, real-valued numeric representation.

#### Embeddings

If you have any sequential discrete data, embedded it. Examples: Words, emojis, website browsing, images, videos, product purchasing …

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

Here are some fetures that we can compute

- Number of times `device_ip` appears on the training data. It would be better if we had `user_id`.
- Number of times `device_ip` appears per month on the training data.
- Min, max, average `C1` per `site_id`.

We can compute these features using `groupby` to aggregate to a new dataframe and then use `merge` to make the new feature.

#### Features based on KNN

K nearest neighbor (KNN) classifier. Looks at the K points in the training set that are nearest to the test input xx and returns the mean of the target variable.

There are many other possibilities here.

### Feature selection

> Way to remove uninformative features.

#### Methods

1. Check correlation
2. Filtering
3. Wrapper methods
4. Embedded methods
5. sklearn `feature_selection`
6. deep learning