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
- etc

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

- k-NN
- Naive Bayes
- Decision Trees
- Support Vector Machines (SVM)
- Logistic Regression

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

- **Clustering** (k-means or Latent Dirichlet allocation (LDA))
- Dimension Reduction (PCA)
- Density estimation (kernel density estimation)
- Matrix Completion (Collaborative Filtering)
- Anomaly Detection (One Class SVM)
- Factor analysis (Exploratory Factor Analysis)

## Parametric v.s. Nonparametric

### Parametric

> Make an assumption about form of the function of the data

* Linear Regression

### Nonparametric

> Do **not** make an assumption about the functional form.

## Steps to fit a model

1. Collect a lot of data
2. Engineer good features
3. Pick a complex algorithm
4. Train the specific model until validation scores starts to go down (smart early stopping).
5. Stop if model meets service level agreement (SLA). Otherwise go back to 1.

### Data <data set>

Lots of data: minimum 30-100 examples <instance / sample> per target to make robust estimates.

#### Clean data

Because ML just learns patterns <attribute / feature>, noisy data makes it hard to learn signal, models might learn the noise.

#### Label data

Most algorithms assumes labels

Most labeling is done by humans

### Training

1. Start with a random guess
2. See how wrong you are (loss function)
3. Change the model to be less wrong
4. Repeat 2-3 until "done"

### Predictions

The **goal** of ML is prediction / inference.

Test your predictions on **test data**, data that you already have put to the side during training (Train / Test split). The simplest kind of generalization.

### Performance Metrics

A number that measures how good your model performs.

You want this to be a single number.

Example:

- Accuracy
- Logarithmic Loss
- True Positive / False Positive / True Negative / False Negative
- Precision / Recall / F Score
- Mean Absolute Error (MAE) / Mean Squared Error (MSE)
- etc