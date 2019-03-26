# Distributions

## Discrete Distributions

###DiscreteUniform

The probability of a draw from any interval without the support is proportional to the length of the interval.

###Bernoulli

A trial is performed with probability $p$ of "success", and $X$ is the indicator of success: 1 means success, 0 means failure.

#### PDF

$$

$$

Probability Parameter: $0<p<1$ the probability of success.

###Binomial

The number of "successes" that we will achieve in $n$ independent trials, where each trail is either a success or a failure, each with the same probability $p$ of success (Sum of multiple independent Bernoulli trials).

#### PDF

$$
f(x, \lambda) =
\begin{cases}
\lambda e^{-\lambda x} & x \ge 0 \\
0 & x<0
\end{cases}
$$

Parameters

$0<p<1$ the probability of success;

$n>0$ the number of trails.

###Possion

The number of rare events (low probability events) that occur in that unit of space or time.

#### PDF

$$

$$

Parameters

$\lambda > 0$ the average rate of $\lambda$ occurrences per unit space or time.



###Geometric



###Negative Binominal

###Hypergeometric

## Continues Distributions

###Uniform

### Exponential (Negative Exponential)

The time between events in a Possion point process.

Eg. a process in which occur continuous and independently at a constant average rate.

#### PDF

$$
f(x, \lambda) =
\begin{cases}
\lambda e^{-\lambda x} & x \ge 0 \\
0 & x<0
\end{cases}
$$

Rate Parameter: $\lambda>0$ the rate of changes, reciprocal of mean time.

OR
$$
f(x, \beta) =
\begin{cases}
\frac{1}{\beta} e^{-\frac{x}{\beta}} & x \ge 0 \\
0 & x<0
\end{cases}
$$
Survival Parameter: $\beta>0$ the expected duration of survival of the system is $\beta$ units of time.

### Normal

#### PDF

$$

$$



### Beta

In the Bayesian approach to statistics, parameters are viewed as random variables, to reflect our uncertainty. The prior for a parameter is its distribution for the parameter after observing data. Beta is the conjugate prior of the Binomial because if you have a Beta-distributed prior on $p$ in a Binomial, then the posterior distribution on $p$ given the Binomial data is also Beta-distributed.
$$
X \mid p \sim Bin(n,p) \\
p \sim Beta(a,b) \\
p \mid (X=x) \sim Beta(a+x, b+n-x)
$$

##### Parameters

$\alpha$ the number of success;

$\beta$ the number of failure.

### Cauchy

 