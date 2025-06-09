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

We randomly choose $70\%$ of the dataset to be the training set, and the rest of the dataset to be the test set.

TODO: