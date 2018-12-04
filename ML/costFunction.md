# Cost Function

We can measure the accuracy of our hypothesis function by using a **cost function**.

##Squared error function / Mean squared error

This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

$J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left ( \hat{y}_{i}- y_{i} \right)^2 = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2$

$\min_{\theta_0, \theta_1} J(\theta_0, \theta_1)$

Squared error cost function is a reasonable choice and works well for problems for most regression programs, and is probably the most commonly used one for regression problems.

### Gradient Descent

repeat until convergence {

​	$\theta_j:=\theta_j−\alpha \frac{\partial}{\partial\theta_j} J(\theta_0,\theta_1)$

​	(simultaneously updata $\theta_1, \theta_2,...,\theta_n$)

}

Updating a specific parameter **prior** to calculating another one on the $j^{(th)}$ iteration would yield to a **wrong** implementation.

$\alpha$: learning rate

$\frac{\partial}{\partial\theta_j} J(\theta_0,\theta_1)$: derivative

If $\alpha$ is too small, gradient descent can be slow.

If $\alpha$ is too large, gradient descent can overshoot the minimum. It may fail to converge, or even diverge.

As we approach a local minimum, gradient descent will automatically take smaller steps. So, no need to decrease $\alpha$ over time.

