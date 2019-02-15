---
description: Support Vector Machine
---

# SVM

### Defined

A supervised machine learning algorithm that learns how to separate groups.

**Find the optimal hyperplane that maximums the margin between support vectors**.

### How decision boundaries scale with dimensionality? <a id="How-decision-boundaries-scale-with-dimensionality?"></a>

A **point \(or a scalar\)** in 1 dimension.

A **line \(or a curve\)** in 2 dimensions.

A **hyperplane \(or a manifold\)** in higher dimensions.

### SVMs learn a decision bound <a id="SVMs-learn-a-decision-bound"></a>

![](http://localhost:8888/notebooks/05_svm__kernels/images/discriminative.png)

Find a boundary that divides the classes from each other \(training\).

Use that boundary to predict class membership for new data \(inference\).

### The "Margin" <a id="SVM:-The-&quot;Margin&quot;"></a>

Rather than drawing a zero-width line between the classes, draw a margin around each line of some width.

### Maximize The Margin <a id="SVM:-Maximize-The-Margin"></a>

![](http://localhost:8888/notebooks/05_svm__kernels/images/max_margin.png)

The margin is up to the nearest point of each class.

### Find the Support Vectors <a id="Support-Vector-Machines-(SVM):-Find-the-Support-Vectors"></a>

![](http://localhost:8888/notebooks/05_svm__kernels/images/margin.png)

A SVM solution only depends on the Support Vectors. **Not** on the whole data set.

### Why are SVMs useful? <a id="Why-are-SVMs-useful?"></a>

* Theoretically guaranteed \(convex optimization\) to find globally optimal solution.
* Fast at inference step because of vectorization.
* Model performance only depends on Support Vectors.
  * A low bias algorithm on small data and large data
  * Handles class imbalances

### When should you NOT use SVMs? <a id="When-should-you-NOT-use-SVMs?"></a>

* Need state-of-the-art performance \(Use Deep Learning\).
* Slow to train.
* Noisier datasets that have overlapping classes have unstable estimates.
* Sensitive to regularization and kernel choices.

### SVM Formalism <a id="SVM-Formalism"></a>

![](http://localhost:8888/notebooks/05_svm__kernels/images/formalism_2.png)

![](http://localhost:8888/notebooks/05_svm__kernels/images/formalism_3.png)

SVM is a convex optimization problem.

### Summary

![](https://blog-c7ff.kxcdn.com/blog/wp-content/uploads/2017/02/Margin.png)

