# MLlib

## MLlib

> Use RDD

## ML

> Use DataFrame

Support Pipelines of estimators, transformer and evaluators.

### Main Components

#### Transformers

> Convert a dataset to another.

- Feature transformer: take a DataFrame output a DataFrame with new columns like feature vectors.
- Learning model: take a DataFrame and output a DataFrame with predict labels.
- `transform()`

#### Estimators

> Algorithms that produce transformers by fitting on a dataset.

`fit()`: take a DataFrame and parameters.

#### Evaluators

> Evaluate the performance of a model.

`evaluator()`

#### ML Parameters

> Specify parameters for estimators and transformers.

- Also can use `ParamGridBuilder()` for choosing the model produced by the best-performing set of parameters in `CrossValidator()`. 

#### ML Pipeline

- In machine learning, the same steps are often repeated with slightly different parameters to find the best results. 
- A Pipeline chains multiple Transformers and Estimators together to specify an ML workflow and runs in order. 

- `PipelineModel()`

## Algorithms

**Some of the algorithms are not included because they were not designed for parallel platforms**

### Logistic Regression

### Decision Tree

### Random Forest

### K-Mean Clustering

