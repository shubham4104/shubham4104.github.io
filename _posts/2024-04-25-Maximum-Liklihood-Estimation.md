---
title: "Exploring Maximum Likelihood Estimation"
date: 2024-04-25
permalink: /blog/exploring-MLE
tags: [MLE, Distributions]
---

In this article, we will explore how Maximum Likelihood Estimation correlates data with different probability distributions.

Let's say we have a set of data ($X_1, X_2, X_3, ..., X_n$), and we want to fit the data to a probability distribution. How do we do that?

First, we identify the distribution we want to fit our data to, such as Normal, Poisson, Binomial, Multinomial, etc. These are simple yet fundamentally natural distributions, and we will see how we can fit our data to these distributions.

### Normal Distribution

For the normal distribution, $P(x) = \\frac{1}{(2 \pi \sigma^2)^{1/2}} \exp^{-\\frac{(x-\mu)^2}{2 \sigma^2}}$, also represented as $\mathcal{N}(\mu, \sigma^2)$, where $\mu$ is the mean, and $\sigma^2$ is the variance.

To fit our data to the Gaussian distribution, we need both $\mu$ and $\sigma^2$.

- $\mu$ is the empirical mean:
  $\mu = \\frac{X_1 + X_2 + ... + X_n}{n}$
- $\sigma^2$ is the empirical variance: $\sigma^2 = \\frac{(X_1 - \mu)^2 + (X_2 - \mu)^2 + ... + (X_n - \mu)^2}{n}$

These values make sense naturally since we are accustomed to the Gaussian distribution.

### Poisson Distribution

Similarly, for the Poisson distribution, Poisson($\lambda$), we have:

$P(x=k) = e^{-\lambda} \\frac{\lambda^k}{k!}$

Given the data, we need to estimate the value of $\lambda$ to fit it to the Poisson distribution.

The $E[X] = \lambda, E[X^2] = \lambda$, i.e., the estimated value of both the mean and variance is equal to $\lambda$.

Should we assign $\lambda$ to the empirical mean 
($\\frac{X_1 + X_2 + ... + X_n}{n}$) 
or the empirical variance ($\\frac{(X_1 - \mu)^2 + (X_2 - \mu)^2 + ... + (X_n - \mu)^2}{n}$)?

This suggests that we need a mechanism to better fit our data to these distributions. This is where _Maximum Likelihood Estimation_ comes to the rescue.

[Work in progress...]
