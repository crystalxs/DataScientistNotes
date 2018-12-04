# Feature Engineering

The process of formulating the most appropriate features given the goal, the algorithm, and the raw data.

## 3 common approaches to FE

1. Hand crafted rules
2. Learned models
3. Stacking

###Hand crafted rules

A good place to start

Very common

Requires domain expertise

Examples: The "magic numbers" in filtering / thresholding

###Learned

Apply ML to Feature Engineering

Typically unsupervised

### Stacking

The outputs of one model become the inputs of another model

```python
Pipeline = [Transformer, Transformer, Transformer]
```

## Commom FE techniques

- Handling Missing Values
- Vectorizing
- Filtering / Thresholding
- Binning
- Transforming
  - Rescaling
- Feature selection

###Missing Values[¶](http://localhost:8888/notebooks/ml-intro-course/08_features_cross_val_pipelines/3_feature_engineering.ipynb#Missing-Values)

All data has missing values. Just deal with it.

Be very careful that the missing data is not systematic of the effect you are studying.

Maybe missing data could be a feature (not a bug).

**(An incomplete) list of techniques:**

- Drop rows (instances)
- Drop columns (features)
- Impute values

Slide Type-SlideSub-SlideFragmentSkipNotes

**Ways to impute values:**

1. Go get the missing data!
2. Sample from existing values
3. Calculated mean of existing values
4. Fit a model on other features to estimate missing value
   - Regression is often used because it is multivariate mean estimation.
   - k-NN works well.
5. Deep Learning