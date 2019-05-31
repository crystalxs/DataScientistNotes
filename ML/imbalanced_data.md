# Imbalanced Data

## Unbalance on Target

### Ignore it

It might not matter (seriously).

Small-ish differences at large scale might not effect business outcomes.

### Resampling

1. Over sample minority group, eg SMOTE
2. Under sample majority group
3. Representative sampling of both groups

### Evaluation Metrics

Avoid accuracy. Use F-score and AUC.

### Robust algorithm

eg. SVM is very robust to class Imbalances.

### Loss function

Weight mistakes for smaller classes more highly than mistakes for larger classes.

#### What is the difference between error and loss?

**Error** is a mistake.

**Loss** is a **weighted** mistake.

## Unbalanced on Features

If we want to split on a feature, it would be best if both features are relatively balanced.

## Unbalanced on Regression

In Regression, we want to predict a value. It is best if all possible values are equally represented.