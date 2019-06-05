# Missing Value

> Be very careful that the missing data is not systematic of the effect you are studying. Maybe missing data could be a feature (not a bug).

#### (An incomplete) Techniques

- Keep it
- Drop rows (instances)
- Drop columns (features)
- Impute values

##### Ways to impute values

- Go get the missing data
- Sample from existing values
- Deep Learning
- Calculated mean/medium of existing values for continue variable
- Calculated majority of existing values for category variable
- Fit a model on other features to estimate missing value
  - Regression is often used because it is multivariate mean estimation
  - k-NN works well