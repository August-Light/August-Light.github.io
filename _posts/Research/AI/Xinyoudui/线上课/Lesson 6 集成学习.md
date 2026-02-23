**集成学习**是一种机器学习思想，它通过组合若干个**弱学习器**得到更好效果。

常见的集成学习有 **Bagging** 和 **Boosting** 这两种。

# 自助采样法

这不属于集成学习，但是是后文中的 Bagging 会用到的东西。

**自助采样法 (bootstrap sampling)**：即有放回采样，对于一个数据集 $D$，我们每次在 $D$ 中随机选择一个样本 $d$ 复制到数据集 $D'$，但是不把 $d$ 从 $D$ 中删除。最终得到 $D'$ 为采到的样。

小结论：$D$ 中约有 $36.8 \%$ 的样本没出现在 $D'$ 中。

$$\lim_{n \to \infty} \left( 1 - \frac 1 n \right)^n = \frac 1 e \approx 36.8\%$$

# Bagging

全称是 **B**ootstrap **Agg**regat**ing**，致敬传奇缩写。

Bagging 用于解决分类的任务。

通过 bootstrap sampling 取出 $D_1, \cdots, D_n$ 这样 $n$ 个数据集，用每个数据集独立地**并行**训练一个分类算法，然后最后**平权投票**表决。

## 随机森林

**随机森林 (Random Forest)** 属于 Bagging 的一个提升。它引入了随机特征选择。

先 bootstrap sampling 随 $n$ 个数据集，在每个数据集内部**再随机选择 $k$ 个特征**用于训练，具体的训练算法一般是 CART 决策树。

# Boosting

搞一个训练集。先训练一个学习器 $1$ 号，然后针对 $1$ 号的不足训练一个学习器 $2$ 号，然后针对 $1,2$ 号的不足训练一个 $3$ 号……最后**加权投票**。

和 Bagging 不同的是，学习器的训练是有顺序的，即**串行**训练。

## AdaBoost

TODO:

**AdaBoost (Adaptive Boosting)**

令 $f(x)$ 为 $x$ 的标准答案：

$$f(x) \in \{-1, +1\}$$

$h_t$ 为训练出来的第 $t$ 个学习器

$D_t$ 为第 $t$ 轮时样本的权重分布

$$\sum_x D_t(x) = 1$$

错误率 $\epsilon_t$：

$$\epsilon_t = P_{x \sim D_t}(h_t(x) = f(x))$$

把权重从 $D_t$ 改成 $D_{t+1}$：

$$\alpha_t = \frac 1 2 \ln \frac {1 - \epsilon_t} {\epsilon_t}$$

$$D_{t+1}(x) = \frac {D_t(x)} {Z_t} \times \begin{cases}
    \exp(- \alpha_t), & h_t(x) = f(x) \\
    \exp(\alpha_t), & h_t(x) \ne f(x) \\
\end{cases}$$

偷个懒：

$$D_{t+1}(x) = \frac {D_t(x)} {Z_t} \times \exp(- \alpha_t f(x) h_t(x))$$



## GBDT

TODO:

## XGBoost

TODO: