# Support Vector Machine

> A supervised machine learning algorithm that learns how to separate groups.

2. 7 SVM
   •        请解释SVM,（似乎任何模型都可能“解释该模型”）
   •        什么是Support vector
   •        请解释kernel trick, 为什么它kernel matrix是正定的
   •        要知道SVM的复杂度依赖于什么，样本量还是变量数
   •        解释SVM模型的几个重要参数



**Find the optimal hyperplane that maximums the margin between support vectors**.

* A **point \(or a scalar\)** in 1 dimension.

* A **line \(or a curve\)** in 2 dimensions.

* A **hyperplane \(or a manifold\)** in higher dimensions.

## Steps

1. Find a boundary that divides the classes from each other \(training\).
2. Use that boundary to predict class membership for new data \(inference\).

### Find the Support Vectors

A SVM solution only depends on the Support Vectors. **Not** on the whole data set.

![margin](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/svm-support-vector.png)

### The Margin

> Rather than drawing a zero-width line between the classes, draw a margin around each line of some width.

The margin is up to the nearest point of each class.

### Formalism

### Kernel Trick

> Take a nonlinear mapping of the data: maps lower dimensional data into higher dimensions. (Hopefully, then the data is **linearly separable** in higher dimensions.)
>
> Then you have an easy-to-fit linear model with lower bias.

#### Disadvantage

- Selecting a reasonable kernel can be hard.
- Since kernels are often nonlinear and involve higher dimensional scaling, there can be high computational cost.

#### Popular Kernals

##### Polynomial Kernel

##### Radial Basis Function Kernel

##### Sigmoid Kernel

## Pro v.s. Con

### Advantage

* Theoretically guaranteed \(convex optimization\) to find globally optimal solution.
* Fast at inference step because of vectorization.
* Model performance only depends on Support Vectors.
  * A low bias algorithm on small data and large data
  * Handles class imbalances

### Disadvantage

* Need state-of-the-art performance \(Use Deep Learning\).
* Slow to train.
* Noisier datasets that have overlapping classes have unstable estimates.
* Sensitive to regularization and kernel choices.
