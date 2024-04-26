---
title: "Fitting Probability Distributions with Maximum Likelihood Estimation"
date: 2024-04-25
permalink: /blog/exploring-MLE
tags: [MLE, Distributions]
---

In this article, we will explore how Maximum Likelihood Estimation correlates data with different probability distributions.

Let's say we have a set of data ($$X_1, X_2, X_3, ..., X_n$$), and we want to fit the data to a probability distribution. How do we do that?

First, we identify the distribution we want to fit our data to, such as Normal, Poisson, Binomial, Multinomial, etc. These are simple yet fundamentally natural distributions, and we will see how we can fit our data to these distributions.

### Normal Distribution

For the normal distribution, $$P(x) = \frac{1}{(2 \pi \sigma^2)^{1/2}} \exp^{-\frac{(x-\mu)^2}{2 \sigma^2}}$$, also represented as $$\mathcal{N}(\mu, \sigma^2)$$, where $$\mu$$ is the mean, and $$\sigma^2$$ is the variance.

To fit our data to the Gaussian distribution, we need both $$\mu$$ and $$\sigma^2$$.

- $$\mu$$ is the empirical mean: $$\mu = \frac{X_1 + X_2 + ... + X_n}{n}$$
- $$\sigma^2$$ is the empirical variance: $$\sigma^2 = \frac{(X_1 - \mu)^2 + (X_2 - \mu)^2 + ... + (X_n - \mu)^2}{n}$$

These values make sense naturally since we are accustomed to the Gaussian distribution.

### Poisson Distribution

Similarly, for the Poisson distribution, Poisson($$\lambda$$), we have:

$$P(x=k) = e^{-\lambda} \frac{\lambda^k}{k!}$$

Given the data, we need to estimate the value of $$\lambda$$ to fit it to the Poisson distribution.

The $$E[X] = \lambda, E[X^2] = \lambda$$, i.e., the estimated value of both the mean and variance is equal to $$\lambda$$.

Should we assign $$\lambda$$ to the empirical mean ($$\frac{X_1 + X_2 + ... + X_n}{n}$$) or the empirical variance ($$\frac{(X_1 - \mu)^2 + (X_2 - \mu)^2 + ... + (X_n - \mu)^2}{n}$$)?

This suggests that we need a mechanism to better fit our data to these distributions. This is where _Maximum Likelihood Estimation_ comes to the rescue.

### Maximum Likelihood Estimation (MLE)  

Let's say we have $$P= P_{\theta} | \theta \in \Theta$$ be the probability distribution. Maximum Likelihood Estimation (MLE) picks the $$\theta \in \Theta$$ that makes the data maximally likely, In other words maximizes $$P(data |\theta) = P_{\theta}(data)$$.  

- For P = Gaussian, $$\theta$$ = $$(\mu, \sigma^2)$$  
- For P = Poisson, $$\theta$$ = $$(\lambda)$$

The goal of MLE is to find this $\theta$. To find these parameters, we write the expression $$\log(P(data | \theta))$$ and solve for $$\theta$$ (Maximizing the log-likelihood is equivalent to maximizing the likelihood).

**Applying MLE to Different Distributions:**

**Poisson Distribution:**  
$$LL(\lambda)$$ = $$\log(P(data | \lambda))$$ = $$\log(P(X_1, X_2, ..., X_n | \lambda))$$ = $$\log(P(X_1 | \theta) * P(X_1 | \theta)...P(X_n | \theta))$$ = $$\log(P(X_1 | \theta)) + \log(P(X_1 | \theta)) + ... + \log(P(X_n | \theta))$$ = $$\log(e^{-\lambda} \frac{\lambda^{X_1}}{X_1!}) + \log(e^{-\lambda} \frac{\lambda^{X_2}}{X_2!}) +...+ \log(e^{-\lambda} \frac{\lambda^{X_n}}{X_n!})$$  
$$LL(\lambda)$$ = $$-n\lambda + (X_1 + X_2 +...+ X_n)*\ln(\lambda) - \ln(X_1! X_2!...X_n!)$$  
$$\frac{dLL(\lambda)}{d\lambda}$ = $-n + \frac{X_1+X_2...X_n}{\lambda}$$  
Setting it to zero, we get $$-n + \frac{X_1+X_2...X_n}{\lambda}$$, $$\implies \lambda = \frac{X_1+X_2...X_n}{n}$$  
This implies that $$\lambda$$ is equal to the empirical mean.

**Gaussian Distribution:**  
$$\mu$$ = $$\frac{X_1+X_2...X_n}{n}$$  
$$\sigma^2$$ = $$\frac{(X_1-\mu)^2 + (X_2-\mu)^2...(X_n-\mu)^2}{n}$$

**Binomial Distribution:**  
$$P(data | p)$$ = $${n}\choose{k}$ $p^k$$ $$(1-p)^{n-k}$$  
$$LL(P(data | p))$$ = $${n}\choose{k}$$ + $$k \ln{(p)}$$ + $$(n-k)\ln{(1-p)}$$  
Setting it to zero, we get $$\frac{dLL}{dp} = \frac{k}{p} -\frac{n-k}{1-p} = 0$$, $$\implies p = \frac{k}{n}$$

Given all the benefits of MLE, it can be biased in finite samples where it diminishes as the sample size increases.

There are other alternatives to MLE:

1. **Maximum Entropy**: Maximum Entropy aims to reduce bias by maximizing entropy under constraints but can still be influenced by the choice of constraints and assumptions.

2. **Bayesian Estimation**: Bayesian estimation's bias depends on the prior distribution choice and its influence on the posterior estimates.

### Conclusion

Maximum Likelihood Estimation is a powerful technique for estimating parameters of probability distributions from data. By maximizing the likelihood function, it finds parameter values that make the observed data most probable. However, MLE can exhibit bias in finite samples, and alternative methods like Maximum Entropy or Bayesian Estimation may be explored to mitigate potential biases or incorporate additional information. Ultimately, the choice of estimation method should consider the problem context, data characteristics, and the trade-offs between bias, variance, and computational complexity.
