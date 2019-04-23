# Loss Function

> Function of the true parameters and the estimated values.

$L(\theta, \hat{\theta})=f(\theta, \hat{\theta})$

### Squared

$L(\theta, \hat{\theta})=(\theta-\hat{\theta})^2$

### Asymmetric Squared

$L(\theta, \hat{\theta}) = \begin{cases} (\theta-\hat{\theta})^2 & \hat{\theta} < \theta \\ c(\theta-\hat{\theta})^2 & \hat{\theta} \geq \theta \end{cases}$

### Absolute

$L(\theta, \hat{\theta}) = \mid \theta - \hat{\theta} \mid$

More robust to outlier in data.

### Zero-One

$L(\theta, \hat{\theta}) = \begin{cases} 1 & \theta \neq \hat{\theta} \\ 0 & \theta = \hat{\theta} \end{cases}$

Use often in binary classification.

### Log

$L(\theta, \hat{\theta}) = - \theta log(\hat{\theta}) - (1-\theta) log(1-\hat{\theta}) \; \theta \in \{0,1\}, \hat{\theta} \in [0,1]$

## Bayesian Aim: minimizing expected loss

$$
E_{\theta}[L(\theta, \hat{\theta})]
$$

- Bayesian inference takes into account the variability of the loss function over $\theta$.
- Frequentist analysis only looks at one value of the loss.

##### Pseudo-Code:

For i = 1:N
	sample $\theta_i \sim p(\theta \mid y)$

Approximate $\hat{L}(\hat{\theta}) = \frac{1}{N} \sum_{i=1}^N L(\theta, \hat{\theta})$

