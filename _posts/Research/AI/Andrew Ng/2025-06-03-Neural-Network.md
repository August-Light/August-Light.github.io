---
title: "Neural Network"
date: 2025-06-03
permalink: /posts/2025/06/Neural-Network/
excerpt: "Intro to Neural Network."
tags:
  - Andrew Ng
---

# Neural Network

When learning complex nonlinear hypotheses, there are too many high degree terms so that it's not a good idea to do so. Neural Network is here to solve this.

## Terms about NN

**Activation function (激活函数)** is a term that refers to the non-linear function used in the model, e.g. sigmoid.

**Weights (权重)** is the $\theta$.

The first layer of all the layers is called the **input layer (输入层)**, the last layer is called the **output layer (输出层)**, and the remaining layers are called the **hidden layers (隐藏层)**.

## Symbols

$a^{(j)}_i$ is the activation of unit $i$ in layer $j$.

$\Theta^{(j)}$ is the matrix of weights controlling function mapping from layer $j$ to layer $j+1$.

Denote $s_j$ as the number of nodes in the $j$-th layer (not including $a^{(j)}_0$). The size of the matrix $\Theta^{(j)}$ should be:

$$s_{j+1} \times (s_j + 1)$$

## Forward-Propagation of NN

We start with $z^{(1)} = x$.

For each layer $j$:
- $z^{(j)} = \Theta^{(j-1)} z^{(j-1)}$
- $a^{(j)} = \sigma(z^{(j)})$
- Add $a^{(j)}_0 = 1$.

## Learning Algorithm

We define $L$ as the total number of layers, $s_l$ as the number of nodes in the $l$-th layer ($a^{(l)}_0$ excluded), and $K$ as the number of nodes of the output layer (therefore, $K = s_L$).

### Cost Function

Recall the cost function for logistic regression:

$$\text{Cost}(h(x), y) := - y \ln h(x) - (1 - y) \ln (1 - h(x))$$

Therefore, we can write the whole cost function $J(\Theta)$ as

$$\begin{aligned}
    J(\Theta) =& - \frac 1 m \left( \sum\limits_{i=1}^m \sum\limits_{k=1}^K y^{(i)}_k \ln(h_\Theta(x^{(i)}))_k + (1 - y^{(i)}_k) \ln(1 - h_\Theta(x^{(i)}))_k \right) \\
    & + \frac \lambda {2m} \left( \sum\limits_{l=1}^{L-1} \sum\limits_{i=1}^{s_l} \sum\limits_{j=1}^{s_{l+1}} (\Theta^{(l)}_{j,i})^2 \right)
\end{aligned}$$

### How to compute $\frac \partial {\partial \Theta^{(l)}_{i,j}} J(\Theta)$: Back Propagation

- For all $l,i,j$, $\Delta^{(l)}_{i,j} \gets 0$
- For $i \in [1,m]$ (all training data)
  - Perform forward propagation
  - $\delta^{(L)} \gets a^{(L)} - y^{(i)}$
  - For $l$ from $L-1$ to $2$ (Compute $\delta^{(L-1)}$ to $\delta^{(2)}$):
    - $\delta^{(l)} = (\Theta^{(l)})^T \delta^{(l+1)} \odot \sigma'(z^{(l)})$
      - Note: $\odot$ is the Hadamard product.
      - Note: $\sigma'(z^{(l)}) = a^{(l)} \odot (1 - a^{(l)})$.
  - $\Delta^{(l)} \gets \Delta^{(l)} + \delta^{(l+1)} (a^{(l)})^T$

It can be shown that:

If $j=0$,

$$\frac \partial {\partial \Theta^{(l)}_{i,j}} J(\Theta) = \frac 1 m \Delta^{(l)}_{i,j}$$

Otherwise,

$$\frac \partial {\partial \Theta^{(l)}_{i,j}} J(\Theta) = \frac 1 m \Delta^{(l)}_{i,j} + \lambda \Theta^{(l)}_{i,j}$$

Note: when doing gradient descent, each of the elements in $\Theta$ should be assigned a random value within $[-\varepsilon, \varepsilon]$ to break symmetry.

## Details when Implementing NN

A reasonable default of choosing hidden layers is:
- choosing 1 single layer, or
- choosing layers with the same number of hidden units in every layer.

The size of a hidden layer should be comparable to the size of the input (e.g. 1x, 2x, or more).

# Avoid Bugs in Code: Gradient Checking

$$\frac \partial {\partial \Theta^{(l)}_{i,j}} \approx \frac {J(\cdots, \Theta^{(l)}_{i,j} + \varepsilon, \cdots) - J(\cdots, \Theta^{(l)}_{i,j} - \varepsilon, \cdots)} {2 \varepsilon}$$

Note: $\varepsilon = 10^{-4}$ is a reasonable value in practical.

Using this formula we can calculate an approximation for the gradient of $J$, and we compare the approximation to the real gradient we calculated by back propagation.

DO NOT forget to turn off this method when learning, or the code will be really slow.

# Multi-Class Classification with NN

We modify the output $h_\Theta(x)$ into a vector.

For example, if $h_\Theta(x) \approx \begin{bmatrix} 0 \\ 1 \\ 0 \\ 0 \end{bmatrix}$, we know that $x$ is classified into the second class. We take the greatest component of the vector as our final result.

💡 ChatGPT said the sigmoid function should not be used when solving multi-class classification. Instead, this method is more suitable for multi-label classification.