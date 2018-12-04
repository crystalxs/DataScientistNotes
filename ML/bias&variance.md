# Bias vs Variance

## Bias

Bias is the error rate of your model on the **training dataset**.

Bias is how much your model **under-fits** the training data, an algorithm that has a **good** ability to fit the training data has **low** bias.

Parametric models are mostly likely to euroneous assumptions.

###Computation

Expected difference between predicted and observed

$Bias[\hat{f}(x)] = E[\hat{f}(x)-f(x)]$

$Error(Y) = E(\hat{Y}-Y)^2 = E[\hat{f}(x)+\varepsilon-f(x)]^2 = E[\hat{f}(x)-f(x)]^2 + Var(\varepsilon)$

where $E[\hat{f}(x)-f(x)]^2$ is the reducible error, and $Var(\varepsilon)$ is the irreducible error, which come from unmeasured variables and unmeasurable variables.

### Decrease

* Make the model more complex
* Pick a different algorithms

##Variance

Variance is the amount that an algorithm's model will change if a different training data is used.

Variance is an algorithm's **flexibility** to learn patterns in the observed data.

Variance is much your model **over-fits** the training data.