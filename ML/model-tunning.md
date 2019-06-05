# Model Tunning

## Parameters v.s. Hyperparameters

Model **parameters** are learned during training and learned for a specific model on specific data.

Model parameters are always learned that is why it is Machine Learning.

**Hyper-parameters** are properties of the algorithm, set before the start of a training.

Hyperparameters can be picked or learned.

### Machine Learning Training

Feature + Algorithm + Hyperparameters = Model Parameters

**Machine Learning is "Double loop" optimization:**

- Outer loop is Hyperparameter search.
- Inner loop is model parameter search.

### Parameter Search

> You can search for algorithm hyperparameters **the same way** can search for model parameters (it is just much slower).

- Closed form (e.g., OLS)
- 1st order methods (e.g., SGD)
- 2ndorder methods (e.g., Newton's Method)
- Manual Search
- Grid Search
- Random Search
- Bayesian Optimization

#### Grid Search

1. Define a grid with n dimensions, the number of parameters.
2. For each dimension within the grid, define the range of possible values.
3. Step through each combination.
4. At the end, choose the best combination of parameters measured on cross-validation dataset.

##### Groups (Strings)

> Using `list`.

Example with Random Forest:

- max_features: ['auto', 'sqrt', 'log2']
- criterion: ['gini', 'entropy']

##### Numeric (Integers or Floats)

> Select a finite set of "reasonable" values, using `range` or `np.array`.

Example with Random Forest:

- n_estimators
- max_depth
- min_samples_split
- max_leaf_nodes

## Pipeline

- Pipelines makes code more readable
- Pipelines makes it easy to change the order or add/remove steps
- You only have to call `fit` and `predict` once
- Easy to write grid search over multiple parameters

### scikit-learn's Transformer class

>For data preparation, [Dataset transformations](https://scikit-learn.org/stable/data_transforms.html)

`fit` – find parameters from training data (if needed)
`transform` – apply to training or test data

### scikit-learn's Estimator class

> For modeling

`fit` – find parameters from training data
`predict` – apply to training or test data

Examples: LR, k-NN, SVM, DT,...

### scikit-learn's Pipeline class

`Pipeline` manage Machine Learning workflows

Examples:
`Pipeline = [Estimator]`
`Pipeline = [Transformer, Transformer, Estimator]`
`Pipeline = [Transformer, Transformer, Transformer]`

![img](https://iaml.it/blog/optimizing-sklearn-pipelines/images/pipeline-diagram.png)