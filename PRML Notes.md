# PRML Notes
[TOC]

## 1. Introduction
### 1.1 Example: Polynomial Curve Fitting

We fit the data using the polynomial function of the form ($y$ for predictor function and $t_n$ for independent values)

$$y(x,\mathbf{w}) =  \sum_{j=0}^M w_j x^j$$
and try to minimize

$$E(\mathbf{w}) = 
\frac 12 \sum_{n=1}^N \left\{ y(x_n, \mathbf{w}) - t_n \right\}^2$$

In order to measure error from different sample sizes into the sample space (and unit), we use Root Mean Square (RMS):

$${E}_{RMS}=\sqrt{2{E}(\mathbf{w^*})/N}$$

Intuitively, **more flexible polynomials with larger values of $M$ are becoming increasingly tuned to the random noise on the target values. The larger the data set, the more complex the model that we can afford to fit to the data.**

The least squares approach to finding the model parameters represents a specific case of MLE, and over-fitting problem can be understood as a general property of MLE.

When we introduce penalty:

$$
\tilde E(\mathbf{w})= \frac 12 \sum_{n=1}^N \left\{ y(x_n, \mathbf{w}) - t_n \right\}^2 + \frac\lambda 2 ||\mathbf{w}||^2$$

Now in effect $\lambda$ controls the effective complexity of the model and hence determines the degree of over-fitting (for any given degree M)

### 1.2.3 Bayesian probabilities
we use machinery of probability theory to describe the uncertainty in model parameters such as $\mathbf{w}$, or indeed in the choice of model itself.

Bayes' theorem was used to convert a prior probability into a posterior probability by incorporating the evidence provided by the observed data.

$$
p(\mathbf w|D) = \frac{p(D|\mathbf w)p(\mathbf w)}{p(D)}
$$

$p(D|\mathbf w)$ is called the *likelihood function*, whose integration over $\mathbf w$ does no sum up to one (w.r.t. $D$ does)

$$\text{posterior}\propto \text{likelihood} \times \text{prior}$$

Both Bayesian and frequentist treat the likelihood function importantly. However, the manner in which it is used is **fundamentally different**.

* In **frequentist setting**, $\mathbf w$ is considered to be a fixed parameters, whose value is determined by some form of "estimator", and the error bar on this estimate are obtained by considerig the distribution of possible data sets $D$.
* **Bayesian** view that there is only a single data set $D$ (which is the one that is actually observed), and the uncertainty in the parameters is expressed through a probability distribution over $\mathbf w$.



