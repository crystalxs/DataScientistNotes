# 1.4. Random Forest

## Algorithm

1. Bootstrap sample: the default is to have the randomly selected data be the same size as the initial dataset, limit each node of the Decision Tree to only consider splitting on a random subset of the features.
2. Build a Decision Tree with each new resample, and at each split bootstrap variables.
3. Vote: probably the most common ensemble method.
4. Prediction: To classify a new datapoint, use each tree in the forest to get a prediction. Choose the category that gets the most votes.

### Reasonable defaults for feature limits (m)

Classification: $m = \sqrt{p}$

Regression: $m = \frac{p}{3}$

*Where p is the total number features, m is a hyper-parameter that can be learned.*

## Model

### Sklearn

> https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html

```python
from sklearn.ensemble import RandomForestClassifier

features_train, labels_train, features_test, labels_test
rf = RandomForestClassifier()
rf.fit(features_train, labels_train)
rf.score(features_test, labels_test)
```

### Feature importance

If a features is higher in a tree, the more important it is in classifying the data.

The expected fraction of data points that reach a node can be used as an estimate of that feature's importance for that tree.

Those values can be averaged across all trees to get the feature's importance.

Given that each feature is measured on a ratio scale, we are able to the relative percentages or one feature 'x' times better than another feature.

```python
feature_importance = dict(zip(iris.feature_names, rf.feature_importances_))
for name, importance in sorted(feature_importance.items(), key=lambda x: x[1], reverse=True):
    print(f"{name:<17}: {importance:>6.2%}")
```

## Adavantage

- Same advantages as Decision Trees
- Robust to overfitting
- Robust to missing variables
- Easy to interpret
- Often perform very well with almost no parameter tuning
- Performance is among the best for traditional ML algorithms
- Can be parallelized for distributed computing

## When should we not use RF

* Small data, especially when the total n is small.
* Also if we need every feature to learn (i.e., extremely heterogeneous data).