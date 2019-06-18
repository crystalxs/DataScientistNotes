# Gradient Boosting

## Boosting Regression

### Algorithm

1. Initialize $f_0(x) = argmin_{\beta} \sum_{i=1}^N L(y^{(i)}, \beta)$.
2. For $m=1$ to M:
   1. Compute the point-wise negative gradient of the loss function at the current prediction $f_{m-1}(x)$, $r_i = -[\frac{\partial L(y,f)}{\partial f}]_{f=f_{m-1} (x^{(i)}), y = y^{(i)}}$ for $i=1,2,…,N$.
   2. Approximate the negative gradient by fitting a regression tree to the targets $r=(r_1,…,r_N)$ giving terminal regions $R_{j_m}, j = 1, …, J_m$.
   3. Compute new predictions for every terminal node. For $j=1….J_m$ compute $\beta_{j_m} = argmin_\beta \sum_{x^{(i)} \in R_{j_m}} L(y^{(i)}, f_{m-1}(x^{(i)}+\beta))$.
   4. Update $f_m(x) = f_{m-1}(x)+\sum_{j=1}^{J_m} \beta_{j_m} 1_{x \in R_{j_m}}$.
3. Return $f(x)=f_M(x)$.

|               | MsE                                             | MAE                                                          |
| ------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| $f_0 (x)$     | $f_0(x) = mean(y^{(i)})$                        | $f_0 (x) = median(y^{(i)})$                                  |
| $r_i$         | $r_i = y^{(i)}-f_{m-1}(x^{(i)})$                | $r_i = sign(y^{(i)}-f_{m-1}(x^{(i)}))$                       |
| $\beta_{j_m}$ | $\beta_{j_m} = mean_{x^{(i)} \in R_{j_m}}(r_i)$ | $\beta_{j_m} = median_{x^{(i)} \in R_{j_m}} (y^{(i)} - f_{m-1}(x^{(i)}))$ |

## Regularization & Under-fitting

### Regularization

> $f_m(x) = f_{m-1}(x)+ \nu T(x; \theta_m)$

Learning Rate $\nu$

- Decrease learning rate need to increase the number of tree ($M$)

## Model