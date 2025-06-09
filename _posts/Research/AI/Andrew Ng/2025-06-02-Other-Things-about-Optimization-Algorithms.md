---
title: "Other Things about Optimization Algorithms"
date: 2025-06-02
permalink: /posts/2025/06/Other-Things-about-Optimization-Algorithms/
excerpt: "Feature Scaling, Choosing Learning Rate, and Regularization."
tags:
  - Andrew Ng
---

# Tricks about Gradient Descent

## Feature Scaling

The goal of this method is to get every feature ($x^{(i)}_j$) into approximately $[-1, 1]$ range.

To be specific, $x_j$ can be replaced with

$$\frac {x_j - \mu_j} {s_j}$$

where $\mu_j$ is the average value of all the $x_j$ in the training set, and $s_j$ is the range of $x_j$.

This method will speed up the algorithm to convergence.

## Choose a good $\alpha$

- If $\alpha$ is too small, that means a slow convergence.
- if $\alpha$ is too large, $J(\theta)$ may not decrease on every iteration; it may even not converge.

To choose $\alpha$, we can try values like:

$$\cdots, 0.01, 0.03, 0.1, 0.3, 1, 3, 10, \cdots$$

# Overfitting

(过拟合)

## Options to reduce overfitting

- Reduce number of features
  - manually select, or
  - model selection algorithm (will be talked about later)
- Regularization
  - reduce magnitude of $\theta_j$
  - works well when we have a whole bunch of features, and every of them contributes a bit to predicting $y$.

## Regularization

We can reduce overfitting by reducing magnitude of $\theta_j$. In order to do this, we can add a term like $+1000\theta_j^2$ to punish the model when it has a too large $\theta_j$.

But in most cases, we don't know which $\theta_j$ we need to punish. Therefore, we can take the cost function like this:

$$J(\theta) = \frac 1 {2m} \left( \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})^2 + \lambda \sum\limits_{j=1}^n \theta_j^2 \right)$$

(By convention, $\theta_0$ is never punished)

$\lambda$ is called the regularization parameter.

The value of $\lambda$ needs to be carefully chosen. In the future, methods for automatically choosing $\lambda$ will be shown.

## Regularization on Normal Equation (Ridge Regression)

$$\theta = \left( X^T X + \lambda \begin{bmatrix}
    0 &   &   &   \\
      & 1 &   &   \\
      &   & \ddots &   \\
      &   &   & 1 \\
\end{bmatrix} \right)^{-1} X^T y$$

Can the matrix in the parenthesis be non-invertible? **Never** (even if $m < n$ or there are linearly-dependent features).

# Other Optimization Algorithms

The video mentioned **Conjugate gradient, BFGS, L-BFGS**.

These algorithms are often more complex, but in return they have some advantages:
- No need to manually pick $\alpha$
- Often faster than gradient descent.

It is suggested that when applying these algorithms, DO NOT write your own code. Instead, try some libraries that others have already done for you.
