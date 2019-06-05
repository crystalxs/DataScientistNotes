# Model

## Supervised Learning

> Learns a mapping from data to labels.

In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.

### Regression

> Predict results within a **continuous** output.
>
> Map input variables to some continuous function. 

**Examples**: predicts real-valued targets

- predict revenue
- predict growth rate
- predict rate of hardware breakdowns

#### Algorithms

- General Linear Model
- Regression Decision Trees
- Regression Support Vector Machines
- [k-NN Regression](https://stats.stackexchange.com/questions/104255/why-would-anyone-use-knn-for-regression)

### Classification 

> Predict results in a **discrete** set of outputs.
>
> Map input variables into discrete categories.

**Examples**: predicts discrete categories

- Classify emails as spam
- Hotdog / Not hotdog in images
- Object identification
- Identify specific people in images

#### Algorithms

- Logistic Regression
- k-NN
- Naive Bayes
- Decision Trees
- Support Vector Machines (SVM)

## Unsupervised Learning

> Learns to identify commonalities in the data.
>
> Learns the hidden (latent) structure of data.
>
> Uses **unlabeled** data (majority of data in the world).

Unsupervised learning allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.

We can derive this structure by clustering the data based on relationships among the variables in the data.

With unsupervised learning there is **no feedback** based on the prediction results.

**Example**:

- **Clustering**
  - k-means
  - Latent Dirichlet allocation (LDA))
- Dimension Reduction (PCA)
- Density estimation (kernel density estimation)
- Matrix Completion (Collaborative Filtering)
- Anomaly Detection (One Class SVM)
- Factor analysis (Exploratory Factor Analysis)

## Parametric v.s. Nonparametric

### Parametric

> Make an assumption about form of the function of the data, such as normal distribution

* Linear Regression
* Logistic Regression
* Naive Bayes

### Nonparametric

> Do **not** make an assumption about the functional form.

* k-NN
* SVM
* Decision Tree

## Steps to fit a model

1. Collect data: minimum 30-100 examples <instance / sample> per target to make robust estimates.
2. Check data
   * Type (memory, category)
   * Duplicate
   * Distribution
   * Imbalance
   * Correlation (perfect multicol 90% -> remove)
   * Missing Value
   * Outlier
3. Train & Test split
4. Feature Engineering
5. Train model
   * Pick model and evaluation metric
   * Tune Hyper-parameter

### Inductive bias

> The set of assumptions that the learner uses to predict outputs given inputs that it has not encountered.

- **Maximum conditional independence**
- **Minimum cross-validation error**
- **Maximum margin**
- **Minimum description length**
- **Minimum features**
- **Nearest neighbors**