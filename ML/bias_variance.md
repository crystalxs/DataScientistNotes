# Bias v.s. Variance

## Bias

> Bias is the error rate of your model on the **training dataset**.
>
> Bias is how much your model **under-fits** the training data, an algorithm that has a **good** ability to fit the training data has **low** bias.

### Computation

> Expected difference between predicted and observed.

$$
Error(Y) = E(\hat{Y}-Y)^2 \\
= E[\hat{f}(x)+\varepsilon-f(x)]^2 \\
= E[\hat{f}(x)-f(x)]^2 + Var(\varepsilon) \\
Bias[\hat{f}(x)] = E[\hat{f}(x)-f(x)]
$$

* $E[\hat{f}(x)-f(x)]^2$ is the reducible error;
* $Var(\varepsilon)$ is the irreducible error, which come from unmeasured variables and unmeasurable variables.

### Decrease

- Make the model more complex;
- Pick a different algorithms.

## Variance

> Variance is the amount that an algorithm's model will change if a different training data is used.
>
> Variance is an algorithm's **flexibility** to learn patterns in the observed data. Variance is much your model **over-fits** the training data.

### Computation

Variance is how much worse you do on the test dataset compared to the training dataset.
$$
Var[\hat{f}(x)]=E[\hat{f}(x)^2]-(E[\hat{f}(x)])^2
$$

### Decrease v.s. Increase

- Model complexity will increase variance;
- Decrease:
  - Feature Selection
  - Regularization
  - Dimensionality Reduction
  - Bagging methods (e.g., Random Forest)

#### Regularization

> The process of introducing additional information to minimize overfitting.
>
> Regularization discourages unnecessary complexity, reduce variance.

##### Ways

1. More data
2. Cleaner data
3. Early stopping
4. Pruning
5. Dropout
6. Resampling the data
7. Add noise to the data (e.g., data augmentation)
8. Adding a constraint to the loss function

##### Constraint to the loss function

Regularized loss = loss function + constraint

By adding a regularization penalty, our objective becomes to minimize the cost function under the constraint that we have to stay within our "budget".

**L1 Regularization**: penalize large coefficients, large coefficients will increase the size of the total error functions.
$$
L1: \lambda ||w||_1 = \lambda \sum_{j=1}^m |w_j|
$$

* Shrink the weights using the absolute values of the weight coefficients (i.e., the weight vector).
* Penalize the model by the absolute weight coefficients.

![l1](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/l1-regularization.png)

**L2 Regularization**: penalize large coefficients, large coefficients will increase the size of the total error functions.
$$
L2: \lambda ||w||_2 = \lambda \sum_{j=1}^m w_j^2
$$

- Shrink the weights by computing the Euclidean norm of the weight coefficients (the weight vector).

![l2](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/l2-regularization.png)

**Regularization parameter $\lambda$**: controls the regularization strength, aka the size of the shaded area. The larger the value of the stronger the regularization of the model.



## Trade Off

**Goal** of Machine Learning:

* Low bias (model the patterns in the observed data)
* Low variance (not sensitive to specificities of the observed data)

![alkeM](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/bias_variance.png)