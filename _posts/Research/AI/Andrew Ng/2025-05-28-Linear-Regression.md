---
title: "Linear Regression"
date: 2025-05-28
permalink: /posts/2025/05/Linear-Regression/
excerpt: "Methods of solving Linear Regression."
tags:
  - Andrew Ng
---

# Univariate Linear Regression

(单变量线性回归)

We guarantee that $m$ is the size of the training set，all the $x^{(i)}$ are inputs，and all the $y^{(i)}$ are outputs。

## Problem

Given the values of a function $f$ at $m$ specific input $x^{(i)}$, which are denoted as $y^{(i)}$ ($i \in [1,m]$).

I want my algorithm to give me a **hypothesis function** $h_\theta(x)$ (abbreviated as $h(x)$), where $h_\theta(x) = \theta_0 + \theta_1 x$ is a linear function, and it should be able to *predict* $f(x)$ for any given $x$.

---

According to the formula of the hypothesis function (and by some statistics knowledge), we can say that the function is good if the value of this function is minimized:

$$J(\theta) := \frac 1 m \sum\limits_{i=1}^m \text{Cost}(h_\theta(x^{(i)}), y^{(i)})$$

where

$$\text{Cost}(h(x), y) := \frac 1 2 (h(x) - y)^2$$

The function $J$ is called the **squared error (cost) function**。

💡Why there is a constant $\frac 1 2$? Well, it is just used to simplify the derivative operation which we will do in the next part.

## Solution

When minimizing a multi-variable function, a method called **Gradient Descent (梯度下降)** is often used.

This is the pseudocode for Gradient Descent:

```
θ ← θ_init
repeat until convergence {
    grad ← ∇J(θ)
    θ ← θ - α * grad
}
```

$\nabla J(\theta)$ is the gradient of $J$ at position $\theta$.

The parameter $\alpha$ is called the learning rate (学习率). It determines how big a step we will take. If $\alpha$ is too small, the algorithm can be too slow; however, if $\alpha$ is too big, the algorithm may overshoot the minimum or even do not converge.

It is worth mentioning that there is no need to decrease $\alpha$ as the algorithm is running. The algorithm will automatically use smaller steps when approaching a local minimum.

### How can I use it in Linear Regression?

$$\frac \partial {\partial \theta_0} J(\theta_0, \theta_1) = \frac 1 m \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})$$

$$\frac \partial {\partial \theta_1} J(\theta_0, \theta_1) = \frac 1 m \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)}) \times x^{(i)}$$

Notice that $J$ is a convex function. Therefore, the gradient descent algorithm will always converge on the absolute minimum (as long as $\alpha$ is not too large).

💡 If a function is not convex but only has one local minimum, we cannot guarantee the algorithm converges on the absolute minimum. Plateaus can really slow down our algorithm.

### What's more

Our algorithm is actually called the *Batch* Gradient Descent. The word *batch* means that we look at the whole bunch of dataset when calculating the gradient.

Compared to other methods like the Normal Equations Method (which we are going to talk about in the next part), gradient descent is more efficient so it performs better on large datasets.

# Multivariate Linear Regression

(多元线性回归)

We guarantee that $m$ is the size of the training set，all the $x^{(i)}$ are vector inputs，and all the $y^{(i)}$ are outputs. $x^{(i)}_j$ is the $j$-th component of vector $x^{(i)}$.

## Problem

A function $f$ takes an $n$-dimensional vector as the input. Given the values of $f$ at $m$ specific inputs $x^{(i)}$, which are denoted as $y^{(i)}$ ($i \in [1,m]$). $x^{(i)}_0$ is defined as $1$ for any $i$ (therefore, $x^{(i)} \in \mathbb R^{n+1}$).

I want my algorithm to give me a hypothesis function $h_\theta(x)$ (abbreviated as $h(x)$), where $h_\theta(x) = \theta^T x$ is a linear function, and it should be able to *predict* $f(x)$ for any given $x$.

The function $h$ should minimize the following value:

$$J(\theta) := \frac 1 m \sum\limits_{i=1}^m \text{Cost}(h_\theta(x^{(i)}), y^{(i)})$$

where

$$\text{Cost}(h(x), y) := \frac 1 2 (h(x) - y)^2$$

## Solution

We implement the same code for Gradient Descent

```
θ ← θ_init
repeat until convergence {
    grad ← ∇J(θ)
    θ ← θ - α * grad
}
```

We use this formula to calculate $\nabla J$:

$$\frac \partial {\partial \theta_j} J(\theta) = \frac 1 m \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)}) \times x^{(i)}_j$$

# Normal Equations Method

It is a pure linear algebra solution for Linear Regression. The time complexity of this method is $\Theta((m+n)n^{\omega-1})$, where $\omega$ is the exponent of the time complexity of matrix multiplication. Usually, $\omega = 3$.

Suppose you have a $m \times (n+1)$ matrix $X$, and each of the element is defined as:

$$X_{i,j} = x^{(i)}_j, \forall i \in [1,m] \text{ and } j \in [0,n]$$

It turns out to be that the optimal $\theta$ is:

$$\theta = (X^T X)^{-1} X^T y$$

Can $X^T X$ be non-invertible? **Yes**. It happens when:
- **there are linearly dependent features** or
  - e.g., $x_1$ is the size in feet and $x_2$ is the size in meters.
- $m < n$.