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
- Replacing missing values
  - mean/medium of existing values for continue variable
  - recent/majority of existing values for category variable
  - -999 works for tree-based methods
  - reconstruct mission value (train a model on other features to estimate missing value)
    - Regression is often used because it is multivariate mean estimation
    - k-NN works well
- Missing values can be hidden from `isna` (replaced by a number 9999 or ?)
- Add a new column `is_null` for every feature with missing values.
- Treat categories present in the test data but not present in the train data as missing values.
- Some methods like XGBoost can handle missing values.