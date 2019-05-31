# Model Evaluation Procedures

## Training and testing on the same data

> Use **all** your data for training, there no data held out for testing.

Rewards overly-complex models that overfit the training data.

Might not necessarily generalize.

### When

- Have very little data to begin with
- Very small time budget (e.g., learning in a real-time system)
- Sure that the new data is the same as the training data

## Train/test split

> Split the dataset into two sets, the model is trained and tested on different data.

* **Training set**: Data points used to train the model.
* **Testing set**: Data points used to check the performance once training is **completely finished**.

Better estimate of out-of-sample performance, but still a could be a high variance estimate.

Useful because:

- Common
- Simple
- Flexible
- Fast

## Cross Validation

> https://scikit-learn.org/stable/modules/cross_validation.html
>
> Do **not** use all your data for training.

Split your data into 3 separate groups:

* **Test set**: final dataset evaluation with final metric, check the performance once training is **completely finished**;
* **Training set**: dataset with a specific hyperparameter configuration; data points used to train the model;
* **Validation set**: paired with an training to test generalization of each set of hyperparameters; data points to keep checking the performancee of your model in order to improve training.

### Common uses of validation set

- Compare different hyperparameter configurations
- Compare different feature engineering representations or feature selection
- Compare different algorithms
- Estimate Variance (e.g., average model performance)

### k-fold CV

* The training set is split into k smaller sets.
* A model is trained using k-1 of the folds as training data.
* The final model is tested on the completely hold-out test data (the last k split).

#### Common Sizes for Train Test Splits

| Train | Test |
| ----- | ---- |
| 70    | 30   |
| 80    | 20   |
| 90    | 10   |

Mostly an empirical choice based on domain complexity and size of the data.

#### Common Sizes for Folds

- k=5
- k=10 (tends to be the most popular)

Again, an empirical choice based on how many hyperparameters and size of the data.

#### Stratified Sampling

For **classification** problems, stratified sampling is recommended for creating the folds. Each target class should be represented with equal proportions in each of the K folds.

#### sklearn

```python
from sklearn.model_selection import KFold
kf = KFold(n_splits=5, shuffle=False).split(range(20))

print(f"{'Iteration'} {'Training set observations':^48} {'Validate set observations'}")
for iteration, data in enumerate(kf, start=1):
    print(f"{iteration:^9} {data[0]} {data[1]}")
```