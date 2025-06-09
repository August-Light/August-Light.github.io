---
title: "Classification"
date: 2025-06-01
permalink: /posts/2025/06/Classification/
excerpt: "Methods of Classification."
tags:
  - Andrew Ng
---

# Classification - Logistic Regression

## Problem

The values of a function $f$ for $m$ inputs ($x^{(1 \sim m)}$) are given, denoted by $y^{(1 \sim m)}$. The return value of $f$ must only be $0$ or $1$.

I want my algorithm to design a hypothesis function $h_\theta(x)$ to predict the probability for the function $f$ to give $1$ for a particular input $x$.

The hypothesis function should have the form:

$$h_\theta(x) = \sigma(\theta^T x)$$

where $\sigma$ is defined as

$$\sigma(x) = \frac 1 {1 + e^{-x}}$$

According to the form of the hypothesis function and some statistics knowledge, the hypothesis function should minimize $J(\theta)$ for this cost function:

$$\text{Cost}(h(x), y) := - y \ln h(x) - (1 - y) \ln (1 - h(x))$$

An alternative form for this formula is

$$\text{Cost}(h(x), y) := \begin{cases}
    - \ln h(x) & y = 1 \\
    - \ln (1 - h(x)) & y = 0 \\
\end{cases}$$

### Decision Boundary

Inputs which fits the condition $h_\theta(x) \ge \frac 1 2$ is separated with inputs which does not fit the same condition by a boundary called the **decision boundary (决策边界)**.

The decision boundary is a property of $h_\theta$, not the training set.

## Solution

Notice that the cost function is convex, therefore, it is a great function for gradient descent.

We can calculate the Gradient Descent formula for Logistic Regression:

$$\frac \partial {\partial \theta_j} J(\theta) = \frac 1 m \sum \limits_{i=1}^m h_\theta(x^{(i)} - y^{(i)}) x^{(i)}_j$$

# Multi-Class Classification

Train a logistic regression $h_\theta^{(i)}(x)$ for each $i$.

For a input $x$, take

$$\arg \max\limits_i h_\theta^{(i)}(x)$$

as the answer.