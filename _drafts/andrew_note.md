全文使用中英文混着记笔记。

# 1

## Supervised Learning (监督学习)

给你一个已有的数据集，预测新的数据。

- Regression (回归): 预测一个连续值
  - e.g. 预测房价
- Classification (分类): 预测一个离散值
  - e.g. 预测肿瘤是良性还是恶性

## Unsupervised Learning (无监督学习)

给你一个数据集，要你给出这个数据集的结构。

- Cluster (聚类)
  - e.g. Market segmentation
- Cocktail Party Problem Algorithm: 分离混合的音频

# Univariate Linear Regression (单变量线性回归)

符号约定：$m$ 为训练集大小，所有 $x^{(i)}$ 为 input，所有 $y^{(i)}$ 为 output。

## Problem

给定了一个函数 $f$ 在 $m$ 个特定的 input $x$ 处的值，即 $y$。

我希望我的算法能为我设计一个 Hypothesis function $h_\theta(x)$（简称 $h(x)$），其中 $h_\theta(x) = \theta_0 + \theta_1 x$ 是一个一次函数。

函数 $h(x)$ 要能够"较好"地预测 $x$ 处的函数值。

---

According to the formula of the hypothesis function (and by some statistics knowledge), we can say that the function is good if the value of this function is minimized:

$$J(\theta) := \frac 1 m \sum\limits_{i=1}^m \text{Cost}(h_\theta(x^{(i)}), y^{(i)})$$

where

$$\text{Cost}(h(x), y) := \frac 1 2 (h(x) - y)^2$$

The function $J$ is called the Squared error (cost) function。

💡Why there is a constant $\frac 1 2$? Well, it is just used to simplify the derivative operation which we will do in the next part.

## Solution

When minimizing a multi-variable function, a method called Gradient Descent is often used.

### Gradient Descent (梯度下降)

```
θ ← θ_init
repeat until convergence {
    grad ← ∇J(θ)
    θ ← θ - α * grad
}
```

The parameter $\alpha$ is called the learning rate (学习率). It determines how big a step we will take.

If $\alpha$ is too small, the algorithm can be too slow; however, if $\alpha$ is too big, the algorithm may overshoot the minimum or even do not converge.

It is worth mentioning that there is no need to decrease $\alpha$ as the algorithm is running. The algorithm will automatically use smaller steps when approaching a local minimum.

### What about this problem?

$$\frac \partial {\partial \theta_0} J(\theta_0, \theta_1) = \frac 1 m \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})$$

$$\frac \partial {\partial \theta_1} J(\theta_0, \theta_1) = \frac 1 m \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)}) \times x^{(i)}$$

Notice that $J$ is a convex function. Therefore, the gradient descent algorithm will always converge on the absolute minimum (as long as $\alpha$ is not too large).

💡 If a function is not convex but only has one local minimum, we cannot guarantee the algorithm converges on the absolute minimum. Plateaus can really slow down our algorithm.

### What's more

Our algorithm is actually called the *Batch* Gradient Descent. The word *batch* means that we look at the whole bunch of dataset when calculating the gradient.

Compared to other methods like the Normal Equations Method, which we are going to talk about in the next part, gradient descent is more efficient so it performs better on large datasets.

# Multivariate Linear Regression (多元线性回归)

符号约定：$m$ 为训练集大小，$n$ 为变量个数，所有 $x^{(i)}$ 为 input（其中 $x^{(i)}_j$ 代表第 $j$ 个变量，即 $x^{(i)} \in \mathbb R^n$）所有 $y^{(i)}$ 为 output。

## Problem

The value of function $f$ at $m$ particular position $x^{(i)}$ in a $n$-dimensional space is known, denoted by $y$.

Define $\forall i$, $x^{(i)}_0 = 1$. Therefore, $x^{(i)}$ is now an element of $\mathbb R^{n+1}$.

I want my algorithm to design a hypothesis function $h_\theta(x) = \theta^T x$.

The function $h$ should minimize the following value:

$$J(\theta) := \frac 1 m \sum\limits_{i=1}^m \text{Cost}(h_\theta(x^{(i)}), y^{(i)})$$

where

$$\text{Cost}(h(x), y) := \frac 1 2 (h(x) - y)^2$$

## Solution

```
θ ← θ_init
repeat until convergence {
    grad ← ∇J(θ)
    θ ← θ - α * grad
}
```

$$\frac \partial {\partial \theta_j} J(\theta) = \frac 1 m \sum\limits_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)}) \times x^{(i)}_j$$

# Tricks about Gradient Descent

## Feature Scaling

> Get every feature ($x^{(i)}_j$) into approximately $[-1, 1]$ range.

To be specific, $x_j$ can be replaced with

$$\frac {x_j - \mu_j} {s_j}$$

where $\mu_j$ is the average value of all the $x_j$ in the training set, and $s_j$ is the range of $x_j$.

This method will speed up the algorithm to convergence.

## Choose a good $\alpha$

- If $\alpha$ is too small, that means a slow convergence.
- if $\alpha$ is too large, $J(\theta)$ may not decrease on every iteration; it may even not converge.

To choose $\alpha$, we can try values like:

$$\cdots, 0.01, 0.03, 0.1, 0.3, 1, 3, 10, \cdots$$

# Normal Equations Method

It is a pure linear algebra solution for Linear Regression.

Suppose you have a $m \times n$ matrix $X$, and each of the element is defined as:

$$X_{i,j} = x^{(i)}_j$$

It turns out to be that the optimal $\theta$ is:

$$\theta = (X^T X)^{-1} X^T y$$

Is there a situation that $X^T X$ is non-invertible? Yes. It happens when:
- **there are linearly dependent features** or
  - e.g. $x_1$ is the size in feet and $x_2$ is the size in meters.
- $m < n$.

---

The time complexity of this method is $O(m n^2 + n^3)$.

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

\* Notice that the cost function is convex, therefore, it is a great function for gradient descent.

---

Decision Boundary

Inputs which fits the condition $h_\theta(x) \ge \frac 1 2$ is separated with inputs which does not fit the same condition by a boundary called the **decision boundary (决策边界)**.

The decision boundary is a property of $h_\theta$, not the training set.

## Gradient Descent for Logistic Regression

$$\frac \partial {\partial \theta_j} J(\theta) = \frac 1 m \sum \limits_{i=1}^m h_\theta(x^{(i)} - y^{(i)}) x^{(i)}_j$$

# Multi-Class Classification

Train a logistic regression $h_\theta^{(i)}(x)$ for each $i$.

For a input $x$, take

$$\arg \max\limits_i h_\theta^{(i)}(x)$$

as the answer.

# Other Optimization Algorithms

The video mentioned **Conjugate gradient, BFGS, L-BFGS**.

These algorithms are often more complex, but in return they have some advantages:
- No need to manually pick $\alpha$
- Often faster than gradient descent.

It is suggested that when applying these algorithms, DO NOT write your own code. Instead, try some libraries that others have already done for you.





# Overfitting (过拟合)

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

Will the matrix in the parenthesis be non-invertible? **Never** (even if $m < n$ or there are linearly-dependent features).

# Neural Network

When learning complex nonlinear hypotheses, there are too many high degree terms so that it's not a good idea to do so.



**Activation function (激活函数)** is a term that refers to the non-linear function used in the model, e.g. sigmoid.

**Weights (权重)** is the $\theta$.

The first layer of all the layers is called the **input layer (输入层)**, the last layer is called the **output layer (输出层)**, and the remaining layers are called the **hidden layers (隐藏层)**.


$a^{(j)}_i$ is the activation of unit $i$ in layer $j$.

$\Theta^{(j)}$ is the matrix of weights controlling function mapping from layer $j$ to layer $j+1$.

Denote $s_j$ as the number of nodes in the $j$-th layer (not including $a^{(j)}_0$). The size of the matrix $\Theta^{(j)}$ should be:

$$s_{j+1} \times (s_j + 1)$$

## Forward-Propagation of Neural Network

We start with $z^{(1)} = x$.

For each layer $j$:
- $z^{(j)} = \Theta^{(j-1)} z^{(j-1)}$
- $a^{(j)} = \sigma(z^{(j)})$
- Add $a^{(j)}_0 = 1$.

## Multi-Class Classification with NN

We modify the output $h_\Theta(x)$ into a vector.

For example, if $h_\Theta(x) \approx \begin{bmatrix} 0 \\ 1 \\ 0 \\ 0 \end{bmatrix}$, we know that $x$ is classified into the second class.

## Learning Algorithm

记号约定：$L$ 为总层数，$s_l$ 为第 $l$ 层的节点个数（不包括 $a^{(l)}_0$），$K = s_L$ 为 output layer 的节点个数。

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

## Avoid Bugs in Code: Gradient Checking

$$\frac \partial {\partial \Theta^{(l)}_{i,j}} \approx \frac {J(\cdots, \Theta^{(l)}_{i,j} + \varepsilon, \cdots) - J(\cdots, \Theta^{(l)}_{i,j} - \varepsilon, \cdots)} {2 \varepsilon}$$

Note: $\varepsilon = 10^{-4}$ is a reasonable value in practical.

Using this formula we can calculate an approximation for the gradient of $J$, and we compare the approximation to the real gradient we calculated by back propagation.

DO NOT forget to turn off this method when learning, or the code will be really slow.

## Details when actually Implementing NN

A reasonable default of choosing hidden layers is:
- choosing 1 single layer, or
- choosing layers with the same number of hidden units in every layer.

The size of a hidden layer should be comparable to the size of the input (e.g. 1x, 2x, or more).

# Machine Learning Diagnostic

How to increase the performance of a model:
- Get more training examples
- Try smaller sets of features / Try getting additional features
- Try adding polynomial features ($x_1^2, x_2^2, x_1x_2$, etc.)
- Increase or decrease $\lambda$

The diagnostic is a test that can give you insight to pick one of these.

##

We randomly choose $70\%$ of the dataset to be the training set, and the rest of the dataset to be the test set.