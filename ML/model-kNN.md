# k-Nearest Neighbors

> A supervised, classification, nonparametric, instance-based model.

## What is k-NN

## Assumption

**Nearest neighbors**: assume that most of the cases in a small neighborhood in feature space belong to the same class. Given a case for which the class is unknown, guess that it belongs to the same class as the majority in its immediate neighborhood. This is the bias used in the k-NN. The assumption is that cases that are near each other tend to belong to the same class.

## Pro v.s. Con

### Advantage

- Simple - easy to apply and interpret
- No assumptions about distribution of data - useful for ill-tempered data
- No training
- Relatively high accuracy

### Disadvantage

- High memory requirement - stores all of the data
- Computationally expensive - must compute all distances
- Sensitive to irrelevant features and the feature scaling

## Algorithm

1. Have labeled data
2. Pick k (positive integer)
3. Get new sample to classify
4. Select the k entries that are closest to the new sample
5. Take a simple majority vote to pick category for new sample

### Optimal Value for k

If number classes is even: pick k to be odd to prevent ties;

If number classes is odd: pick k to be even to lessen the chances of ties.

### Distance Metrics

> A numerical measurement of how far apart elements are.

#### Norm function

> A function that takes a vector as an input and returns a scalar value.

#### Distance function

> A function that takes in two vectors as an input and returns a scalar value.

![1_2](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/norm.png)

![p](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/infty-norm.png)

##### 1-norm distance(City Block / Manhattan)

$$
||p-q||_1 = \sum_{i=1}^n |p_i-q_i|
$$

##### 2-norm distance(Eculidian)

$$
||p-q||_2 = \sqrt{\sum_{i=1}^n (p_i-q_i)^2}
$$

##### p-norm distance (Minkowski distance of order p)

$$
||p-q||_p = \sqrt[p]{\sum_{i=1}^n (p_i-q_i)^p}
$$

##### Infinity-norm distance (Chebyshev)

$$
||p-q||_{\infty}=max(|p_i-q_i|)
$$

## Evaluation Metrics & Loss Function

## Regularization & Under fitting

## Train Model

### how to train hyper-parameter

#### k

#### Distance Metric

### scikit-learn

## Metrics