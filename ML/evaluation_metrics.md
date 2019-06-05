# Evaluation Metrics

 a.        Cross-Validation、stratified cross-validation
 b. MSE，MAE，impurity function，cross-entrop，precision, recall, AUC, ROC, F1 … 
•        false positive 和 false negative：给出false positive比false negative更重要的例子 

## Regression

- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)

## Classification

### Accuracy

> Fraction of observations classified correctly

$$
{Accuracy} = \frac{Correct}{Total} \\
Error Rate = \frac{Error}{Total} \\
Accuracy = 1-ErrorRate
$$

#### Limitation

* When the data is imbalances, it will be effected a lot;
* Only show overall measurement, doesn't tell what "types" errors;
* **Null accuracy**: achieved by always predicting the most frequent class, especially for imbalanced data

### Confusion Matrix

|                    | Condition positive | condition negative |
| ------------------ | ------------------ | ------------------ |
| Predicted Positive | TP                 | FP                 |
| Predicted Negative | FN                 | TN                 |

- True Positives (TP): correctly predicted a succesfull outcome / one label
- True Negatives (TN): correctly predicted a lack of an outcome / other label
- False Positives (FP): incorrectly predicted a succesfull outcome (a "Type I error")
- False Negatives (FN): incorrectly predicted lack of an outcome (a "Type II error")

#### Precision

> Fraction of actually positive are labeled correct

$$
Precision = \frac{TP}{TP+FP}
$$

#### Recall

> Fraction of labeled positive are actually correct

$$
Recall = \frac{TP}{TP+FN}
$$

#### F-score

$$
F_1 = 2 \frac{percision \times recall}{percision+recall} \\
F_\beta = (1+\beta^2) \frac{percision \times recall}{\beta^2 percision+recall}
$$



### ROC / AUC

