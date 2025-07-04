---
title: "Machine Learning Diagnostic"
date: 2025-06-09
permalink: /posts/2025/06/Machine-Learning-Diagnostic/
excerpt: "Ways of improving your machine learning result."
tags:
  - Andrew Ng
---

# Machine Learning Diagnostic

How to increase the performance of a model:
- Get more training examples
- Try smaller sets of features / Try getting additional features
- Try adding polynomial features ($x_1^2, x_2^2, x_1x_2$, etc.)
- Increase or decrease $\lambda$

The diagnostic is a test that can give you insight to pick one of these.

## Evaluating a Hypothesis

We randomly choose $70\%$ of the dataset to be the training set, and the other $30\%$ of the dataset to be the test set.

In general, we can calculate the cost function $J$ on the test set to evaluate a hypothesis.

e.g., for a logistic regression, we can use the cost function

$$J(\theta) := \frac 1 m \sum\limits_{i=1}^m \text{Cost}(h_\theta(x^{(i)}), y^{(i)})$$

where

$$\text{Cost}(h(x), y) := - y \ln h(x) - (1 - y) \ln (1 - h(x))$$

In particular, for a 0/1 Classification problem, we can calculate the misclassification error:

$$\text{Cost}(h(x), y) := \begin{cases}
    1 & y = 1 \text{ xor } h(x) \ge \frac 1 2 \\
    0 & \text{otherwise} \\
\end{cases}$$

## Model Selection

Assume we have $10$ models, and we train the $10$ models and run them on the same test set.

Intuitively, one might choose the model that has the minimal $J_{\text{test}}$. However, a model having good performance on this particular test set may not perform well on another new test set.

Therefore, instead of splitting the data into 2 pieces, we split it into 3 pieces: training set ($60\%$), cross validation set (abbreviated as cv, $20\%$), and test set ($20\%$).

When running the algorithm, we pick the model with the $\theta = \arg \min\limits_{\theta} J_{\text{train}}(\theta)$ that minimizes $J_{\text{cv}}(\theta)$, and use $J_{\text{test}}(\theta)$ as the final score.

### Bias Problem & Variance Problem

Suppose the algorithm is not performing well (high $J_{\text{cv}}$ or $J_{\text{test}}$). Is it a bias problem or a variance problem?

- Bias (Underfitting)
  - High $J_{\text{train}}$
  - $J_{\text{cv}} \approx J_{\text{train}}$
- Variance (Overfitting)
  - Low $J_{\text{train}}$
  - $J_{\text{cv}} \gg J_{\text{train}}$

## Regularization

We define

$$J_{\text{train}}(\theta) = \frac 1 {2m} \left( \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})^2 + \lambda \sum\limits_{j=1}^n \theta_j^2 \right)$$

and use the same process as above. Notice that $J_{\text{cv}}$ and $J_{\text{cv}}$ should be added a regularization term - this is just used when using optimization algorithms like Gradient Descent.

So how should $\lambda$ be picked? A reasonable method is trying:

$$0, 0.01, 0.02, 0.04, 0.08, \cdots, 10.24$$

