# Decision Tree

> A supervised, non-parametric model.

The **root** of a decision tree is located on the top, it is the first split.

The **node** do a binary split based a specific value of a specific attribute to minimize entropy.

The **leaf** classifies **all** members in the defined feature space as belonging to a **single** class (decision boundary).

## Type

### Classification Trees

- Predict: class label
- Training: minimize impurity
- Inference: assign majority class label of leaf node

### Regression Trees

- Predict: value
- Training: minimize error (typically mean squared)
- Inference: mean of the leaf node

## Steps

> Decision Trees learn **top-down, greedily, recursively**.
>
> The **goal** of DT is divide the dataset into pure regions.

1. Divide-and-conquer : split the data into subsets;
2. Top-down: from a single split
3. Greedily: choose the split that has results in the most pure feature space
   1. Calculate the entropy of the dataset
   2. For every feature, calculate the entropy for all values
   3. Pick feature and value that has the highest Information Gain

The process stops:

* All instances are in same class (simplest and most often used)
* The number of instances is less than a specified minimum
* The tree is deeper than some minimum
* The improvement of class impurity is less than a specified minimum

DT are **greedy**: find and choose the current best value.

Greedy algorithms can have local minimums. There could be complex / future choice dependent rules that could perform better.

### Information Theory

> How decision tree actually decide.

#### Entropy

> The measure of the uncertainty in a random variable.

##### Shannon Entropy

$$
H=−\sum p(x)log_2 p(x)
$$

##### Binary Entropy

$$
H=−\sum plog_2 p - (1-p)log_2(1-p)
$$

#### Information Gain

> aka, KL Divergence or Relative Gain or Relative Entropy.
>
> **Choose one split over another**: find the attribute that returns the highest information gain (i.e., the most homogeneous branches).

Information Gain = Entropy(parent) - Weighted average of entropy(children)​
$$
Gain(S,A) = Entropy(S) - \sum_{v \in values(A)} \frac{|S_v|}{|S|} Entropy(S_v)
$$

#### Gini Index

> A measure of how often a randomly chosen element from the set would be incorrectly labeled if it was randomly labeled according to the distribution of labels in the subset.

$$
Gini = 1 - \sum_{i=1}^K p_k^2
$$

Properties:

- Maximized when elements are heterogeneous (impure).
- Minimized when elements are homogenous (pure).

#### Classification Error 

$\text{𝐶𝑙𝑎𝑠𝑠𝑖𝑓𝑖𝑐𝑎𝑡𝑖𝑜𝑛 𝐸𝑟𝑟𝑜𝑟}=1−𝑚𝑎𝑥𝑝_𝑘$

where $𝑝_𝑘$ denotes the proportion of instances belonging to class $𝑘$.

![compare](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/dt-information-thoery.png)

#### How would we split for multi-nominal features?

1. Consider all possible pairs of splits. For k classes there are 2k-1-1 splits, which is computationally prohibitive if k is a large number.
2. If there are ordered classes, then we do version of binary search. This reduces the search to k-1 possible splits for k classes.
3. If there are have many ks, a One-Versus-All-The-Rest reduces the search to linear for number of k.

#### How would we split for continuous features?

We need a threshold split (i.e., x ≤ 42)

One option is to sort the data and perform binary search for optional split value.

This could be computational intractable because it requires sorting $O(nlogn)$ then binary search $O(logn)$.

### Avoid overfitting

* Acquire more training data
* Pruning
* Setting the maximum depth of the tree
* Setting the minimum number of samples required at each leaf node
* Setting how much IG required to make another split

## Pro v.s. Con

### Advantages

- Simple to use (explain and visualize)
- DT requires little data preparation
- Handle numerical and categorical data
- Handle many types of outputs (regression and multi-class classification)

### Disadvantage

- **Easily overfit**

## Sklearn

https://scikit-learn.org/stable/modules/classes.html#module-sklearn.tree

```python
from sklearn import tree
# from sklearn.tree import DecisionTreeClassifier

features_train, labels_train, features_test, labels_test
clf = tree.DecisionTreeClasifier()
clf = clf.fit(features_train, labels_train)
clf.predict(features_test)
```

### Tunning the pararmeters

https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html

```python
class sklearn.tree.DecisionTreeClassifier(criterion=’gini’, splitter=’best’, max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features=None, random_state=None, max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None, class_weight=None, presort=False)
```

`min_samples_split`: minimum number of elements in each leaf.

`min_samples_split` vs overfitting:

### Plot Decision Tree

```python
from IPython.display import Image  
from sklearn.externals.six import StringIO  
from sklearn.tree import export_graphviz
import pydotplus

dot_data = StringIO()
export_graphviz(dt, out_file=dot_data,  
                filled=True, rounded=True, special_characters=True)
graph = pydotplus.graph_from_dot_data(dot_data.getvalue())  
Image(graph.create_png())
```

### `tree_` Attribute

The decision estimator has an attribute called tree_ which stores the entire tree structure and allows access to low level attributes.

```python
# number of node in the dt
n_nodes = dt.tree_.node_count
# id of the left child of the node
children_left = dt.tree_.children_left
# id of the right child of the node
children_right = dt.tree_.children_right
# feature used for splitting the node
feature = dt.tree_.feature
# threshold value at the node
threshold = dt.tree_.threshold
```