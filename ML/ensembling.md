# Ensembling

> Combine multiple ML models to obtain better predictive performance than any of single models could do alone.
>
> Techniques for combining several weak learners to produce a single strong learner.

## Averaging (Blending)

###Simple averaging

(model 1 + model 2) / 2

###Weighted averaging

(model 1 $\times$ weighted + model 2 $\times$ weighted)

###Conditional averaging

Prediction of model 1 if condition else prediction of model 2

## Stacking

> An ensemble learning technique that uses predictions from previous models to build a new model.

### Pipeline

1. First, clustering (or topic modeling).
2. Then fit a separate classifier for each cluster. Different clusters may have different feature importance.

### Metalearner

Metalearner learns the optimal combination of the base learners.

### When to choose

It is generally a good idea to pipe the outputs of one model into the inputs of another model.

However, creating a meta-learner that is able to choose among heterogeneous models is often too complex for the gain in performance.

## Bagging, aka Bootstrap Aggregating

> Fit multiple models in parallel and independently. Each model gets a vote on the final prediction.

### Parameters that control Bagging

* Changing the seed
* Row (Sub)sampling
* Column (Sub)sampling
* Bootstraping
* Shuffling
* Model specific parameters
* Number of models
* parallelism

###Bootstrap Sampling Step

Create samples by sampling with replacement

1. Start with your dataset of size 𝑛n
2. Sample from your dataset with replacement to create 1 bootstrap sample of size 𝑛n which means many of the observations will be repeated
3. Repeat 𝐵B times
4. Each bootstrap sample can then be used as a separate dataset for model fitting

### Aggregating

For **regression** problems (predicting a continuous value), we **average** the values given by all the models.

For **classification** problems (predicting a categorical value), we choose the label with the **most** votes.

####Types of Voting

**Hard voting**: A model is selected from an ensemble to make the final prediction by a simple majority vote for accuracy.

**Soft Voting**: Can only be done when all your classifiers can calculate probabilities for the outcomes. Soft voting averages out the probabilities calculated by individual algorithms.

### Subsetted data

Bagging does **random** partitions.

### Why do Bagging?

- Increases evaluation metric performance.
- Less likely to overfitting since by making slightly different or let say randomized models, we ensure that the predictions do not read very high variance.
- Improves stability of estimates. If ML people ever made error bars, they would be smaller.

### When to choose

If you have time and enough data, bagging is a good choice because it only improves model performance.

## Boosting

> A sequential process, where each subsequent model attempts to correct the errors of the previous models.

### Subsetted data

Boosting samples data with **errors** at a higher preference.

### Algorithms

- XGBoost (Currently, the most popular)
- AdaBoost
- Gradient Boosting Machine (GBM)

### When to choose

Boosting is good idea if highest level model performance is required.

However, it is more complex than Bagging (harder to implement and harder to debug).

## StackNet

