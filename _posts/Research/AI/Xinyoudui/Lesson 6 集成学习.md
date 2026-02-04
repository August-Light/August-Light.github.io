**集成学习**是一种机器学习思想，它通过组合若干个**弱学习器**得到更好效果。

# 自助采样法

这不属于集成学习，但是是后文中的 Bagging 会用到的东西。

**自助采样法 (bootstrap sampling)**：即有放回采样，对于一个数据集 $D$，我们每次在 $D$ 中随机选择一个样本 $d$ 复制到数据集 $D'$，但是不把 $d$ 从 $D$ 中删除。最终得到 $D'$ 为采到的样。

小结论：$D$ 中约有 $36.8 \%$ 的样本没出现在 $D'$ 中。

$$\lim_{n \to \infty} \left( 1 - \frac 1 n \right)^n = \frac 1 e \approx 36.8\%$$

# Bagging

全称是 **B**ootstrap **Agg**regat**ing**，致敬传奇缩写。

Bagging 用于解决分类的任务。

通过 bootstrap sampling 取出 $D_1, \cdots, D_n$ 这样 $n$ 个数据集，用每个数据集独立地训练一个分类算法，然后最后投票表决。

## 随机森林

**随机森林 (Random Forest)** 属于 Bagging 的一个提升。它引入了随机特征选择。

先 bootstrap sampling 随 $n$ 个数据集，在每个数据集内部**再随机选择 $k$ 个特征**用于训练，具体的训练算法一般是 CART 决策树。

# Boosting

TODO:

## AdaBoost

**AdaBoost (Adaptive Boosting)**

TODO:

## GBDT

TODO:

## XGBoost

TODO: