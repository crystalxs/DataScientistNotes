# Evaluation Metrics

 a.        Cross-Validation、stratified cross-validation
 b. MSE，MAE，impurity function，cross-entrop，precision, recall, AUC, ROC, F1 … 
•        false positive 和 false negative：给出false positive比false negative更重要的例子

### Difference between loss (cost) and metric 

**Loss:** objective function that your model will optimize.

**Metric:** (business objective) human interpretable measure of your models performance.

* Metrics may be hard to optimize.
* In some cases loss function and metrics are the same.

- Review of binary, multi-class and multi-label classification 
- Losses and metrics for classification 

## Evaluation Metrics & Loss

>Given a set of data points {$x^{(1)}, ..., x^{(m)}$}, where each $x^{(i)}$ has n features, associated to a set of outcomes {$y^{(1)}, …, y^{(m)}$}, we want to assess a given classifier that learns how to predict y form x.

### Regression

#### Mean Absolute Error (MAE)

> If you have outlier, use MAE will be more robust than MSE.
>
> RMSE and MSE give a relatively high weight to large errors.
>
> MAE measure average model prediction error in units of the variable of interest.

$$
MSE = \frac{1}{N} \sum_{i=1}^N |y^{(i)} - \hat{y}^{(i)}|
$$

#### Mean Squared Error (MSE)

$$
MSE = \frac{1}{N} \sum_{i=1}^N (y^{(i)} - \hat{y}^{(i)})^2
$$

#### Root Mean Squared Error (RMSE)

> Units of the variable of interest.

$$
MSE = \sqrt{\frac{1}{N} \sum_{i=1}^N (y^{(i)} - \hat{y}^{(i)})^2}
$$

#### R square

$$
SST = \sum_{i=1}^m (y_i - \bar{y})^2 \\
SSR = \sum_{i=1}^m (f(x_i) - \bar{y})^2 \\
SSE = \sum_{i=1}^m (y_i - f(x_i))^2 \\
$$

>  How many percentage of variant in y can be explained by the variant in x.

$$
R^2 = \frac{SSR}{SST} = 1-\frac{SSE}{SST}
$$

##### Adjusted R square

> When number of parameters increasing, the $R^2$ will increasing no matter if the performance.

$$
1 - \frac{(1-R^2)(m-1)}{m-n-1}
$$

### Classification

**Soft prediction:** classifier scores often probabilities.

**Hard prediction:** actual labels.

From soft predictions to hard predictions:

$\hat{y}>threshold$

$argmax \hat{y}_j$

##### Binary Classification

> Each image has exactly **one label.** It is binary because we have **two labels**.

$\hat{y} = P(y=cat|x)$ is a single probability.

##### Multi-Class Classification

>Each image has exactly **one label.** It is multi-class because it has **more than two labels**.

$\hat{y} = (\hat{y}_1, …, \hat{y}_K)$ when $\sum_i^K \hat{y}_i = 1$

##### Multi-label Classification

> Each image can have more than one label.

$\hat{y} = (\hat{y}_1, …, \hat{y}_K)$

#### Log Loss

##### Binary

> Assume 0, 1 labels and soft predictions.

$$
- \frac{1}{N} \sum_{i=1}^N y^{(i)} log \hat{y}^{(i)} + (1-y^{(i)}) log(1-\hat{y}^{(i)})
$$

##### Multi-class

> Assume  one-hot encoding of y.

$$
-\frac{1}{N} \sum_{i=1}^N \sum_{j=1}^K y_j^{(i)} log \hat{y}_j^{(i)}
$$

##### Multi-label

$$
-\frac{1}{N} \sum_{i=1}^N \sum_{j=1}^K [y_j^{(i)} log \hat{y}_j^{(i)} + (1-y_j^{(i)}) log(1-\hat{y}_j^{(i)})]
$$

#### Accuracy

> Fraction of correct predictions, assume hard prediction.

$$
{Accuracy} = \frac{Correct}{Total} = \frac{1}{N} \sum_{i=1}^N 1_{y^{(i)}=\hat{y}^{(i)}}\\
Error Rate = \frac{Error}{Total} \\
Accuracy = 1-ErrorRate
$$

##### Limitation

* When the data is imbalances, it will be effected a lot;
* Only show overall measurement, doesn't tell what "types" errors;
* **Null accuracy**: achieved by always predicting the most frequent class, especially for imbalanced data.

#### Confusion Matrix

|                    | Condition positive | condition negative |
| ------------------ | ------------------ | ------------------ |
| Predicted Positive | TP                 | FP                 |
| Predicted Negative | FN                 | TN                 |

- True Positives (TP): correctly predicted a succesfull outcome / one label
- True Negatives (TN): correctly predicted a lack of an outcome / other label
- False Positives (FP): incorrectly predicted a succesfull outcome (a "Type I error")
- False Negatives (FN): incorrectly predicted lack of an outcome (a "Type II error")

##### Precision

> Fraction of actually positive are labeled correct

$$
Precision = \frac{TP}{TP+FP}
$$

##### Recall

> Fraction of labeled positive are actually correct

$$
Recall = \frac{TP}{TP+FN}
$$

##### F-score

$$
F_1 = 2 \frac{percision \times recall}{percision+recall} \\
F_\beta = (1+\beta^2) \frac{percision \times recall}{\beta^2 percision+recall}
$$

#### ROC

> Threshold the model's predicted probabilities at various places between (0,1)

* True positive rate: proportion of positive class correctly predicted.
* False positive rate: proportion of negative class incorrectly predicted.

#### AUC

> Probability the model will score a randomly chosen positive class higher than a randomly chosen negative class.
>
> Area under the curve.

AUC = pairs of observations correctly ordered / (# of 1 * # of 0)

* Only for binary tasks.
* For multi-label classification compute AUC for each task.
* Depending only on ordering of the predictions.

#### Logloss

