---
description: The one weird thing that makes linear classifiers fit better.
---

# kernel trick

### Defined

Take a nonlinear mapping of the data: maps lower dimensional data into higher dimensions.

Then you have an easy-to-fit linear model with lower bias.

Hopefully, then the data is **linearly separable** in higher dimensions.

### What are the disadvantages of kernel methods? <a id="What-are-the-disadvantages-of-kernel-methods?"></a>

* Selecting a reasonable kernel can be hard.
* Since kernels are often nonlinear and involve higher dimensional scaling, there can be high computational cost.

### Kernels as Functions <a id="Kernels-as-Functions"></a>

Computes a dot product between , \(e.g. a measure of 'similarity' between \). 𝑣⃗ 𝑤⃗ 

It turns out that the SVM has no need to explicitly work in the higher-dimensional space.

A kernel function is similarity function over pairs of data points in raw representation.

This is implicitly transform datasets to a higher-dimensional using no extra memory and minimal effect on computation time.



