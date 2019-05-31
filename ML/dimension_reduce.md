# Dimension Reduce

## What is Dimensionality Reduction used for?

### Data compression

> Combine many raw features into a fewer latent features that are meaningful and "similar".

**Why is data compression useful for ML?**

1. Reduce memory / disk space footprint
2. Speedup ML models (training and predicting)
3. Multicolinearity / Redundant features
4. "The Curse of Dimensionality"

### Data visualization

> Humans can only visualize things in 1-3 dimensions, however, interesting data is often high dimensional.

## Principal Component Analysis (PCA)

### One-Dimensional PCA

We want to find a **line** so that the *projection* of the data onto that line:

- Results in points with *maximum variance* as a 1-dimensional data set.
- Results in points *minimizing the total squared distance* to original data

### Two-Dimensional Principal Component Analysis (PCA)

![img](https://stanford.edu/~shervine/images/pca.png)

Project the data into fewer dimensions that maximizes the variance of the projected space.

### Computing Principal Components

The solution to the problem of finding principal components involves the *eigenvalues* and *eigenvectors*of the covariance matrix of the data X.

X is a dataset, which we represent as a $n\times p$ matrix of numbers.

### PCA Steps

#### Standardize the data

$$
x_j^{(i)}
$$



Standardize the data to have a mean of 0 and standard deviation of 1.

Standardize each dimension independently (i.e., j in the formula).

#### Compute the Covariance Matrix

$$
\begin{bmatrix}
Var(x_1) & Cov(x_1, x_2)  \\       
Cov(x_1, x_2)  & Var(x_2) \\
\end{bmatrix}
$$

![img](https://www.riskprep.com/images/stories/portfolio/covar_matrix.gif)

Given that we have standardized the points, the sample covariance matrix is $=\frac{1}{n}X^tX$.

#### Compute the Eigenvectors and Eigenvalues of $Σ$

When the eigenvalue are sorted from high-to-low, the eigenvectors are the principal components of X.

Since Σ is a symmetric, it has a full set of p eigenvectors.

Since Σ is non-negative definite, the eigenvalues are non-negative numbers.

##### Eigenvectors

> The **eigenvectors** of Σ are vectors v that satisfy a relationship like:Σv=λv
>
> The matrix Σ acts as a **scaling** on the vector v.

We found the set of eigenvectors {→ei} of the covariance matrix Σ=1nXTX

These satisfy the equation Σ→ei=λi→ei, where λi is the variance along the direction defined by →ei

Concatenating all these eigenvectors into a matrix E gives us the matrix representing a rotation in feature space.

X in our new coordinates is X′=XET

Our covariance matrix in these new coordinates is

Σ′=1nX′TX′=1n(XET)T(XET)=1nEXTXET=EMET

Σ′=⎡⎢ ⎢ ⎢ ⎢ ⎢⎣λ10⋯00λ2⋯0⋮⋮⋱0000λp⎤⎥ ⎥ ⎥ ⎥ ⎥⎦

#### How do you pick number of components

1. Look for inflection point (e.g., "elbow" method)
2. Set threshold for % of Variance (e.g., 85% of variance)