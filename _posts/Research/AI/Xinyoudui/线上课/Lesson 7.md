# 聚类

无监督学习算法

# 聚类的评估

## SSE (Sum of Squared Errors)

$$SSE = \sum_{i=1}^k \sum_{j \in C_k} \lVert x_j - \mu_i \rVert^2$$

$SSE$ 越小越好。

主要考虑了**簇内聚程度**。

## SC (Silhouette Coefficient)

[Wiki](https://en.wikipedia.org/wiki/Silhouette_(clustering))

对于每一个点 $x_i$，求出：
- $a(i)$ 为同类点到 $x_i$ 的平均距离。
- $b(i) = \min_{i \not \in C_k} \frac 1 {\lvert C_k \rvert} \sum_{j \in C_k} \lVert x_i - x_j \rVert$，为 $x_i$ 到最近的敌对 cluster 的平均距离。
- 定义**轮廓值** $s(i) = \frac {b(i) - a(i)} {\max(a(i), b(i))}$，不难证明 $s(i) \in [-1, 1]$。

求出所有样本的平均轮廓值 $SC$：

$$SC = \frac 1 n \sum_{i=1}^n s(i)$$

$SC$ 越大越好。

感性理解：$a$ 越小说明这个 cluster 越紧密；$b$ 越大说明不同的 cluster 分得越开。因此把这两个减一下，$b - a$ 越大越好。

主要考虑了**簇内聚程度**、**簇间分离程度**。

## CHI (Calinski–Harabasz Index)

[Wiki](https://en.wikipedia.org/wiki/Calinski%E2%80%93Harabasz_index)

计算以下值：
- $WCSS$ (Within-Cluster Sum of Squares)：和 $SSE$ 一个意思。
- $BCSS$ (Between-Cluster Sum of Squares)：$BCSS = \sum_{i=1}^k \lvert C_i \rvert \lVert \mu_i - \bar \mu \rVert^2$，即每个中心到总中心的距离平方和（对 cluster 的大小加权）。

根据以下公式计算 CHI：

$$CH = \frac {BCSS} {WCSS} \frac {n-k} {k-1}$$

$CH$ 越大越好。

感性理解：$WCSS$ 越小说明 cluster 越紧密；$BCSS$ 越大说明不同的 cluster 分得越开；$k$ 越小越好。

主要考虑了**簇内聚程度**、**簇间分离程度**、**质心个数**。

# $k$-means clustering

以 SSE 为目标函数。

- 随机选择 $k$ 个样本点作为初始聚类中心。
- 把每个点分给（欧氏距离）最近的中心。
- 对每个 cluster 将中心设置为所有点的重心。
- 返回第二步，直到不再发生变化。

## 怎么确定 $k$

随着 $k$ 增大，当 cost function 从大幅下降突然变为缓慢下降的点，被认为是最优的 $k$。

这被称为 Elbow method，因为图像看起来像一个手肘。

# Naive Bayes Classifier

TODO:

由于我们是已知 $x_1, \cdots, x_n$ 要求 $C_k$ 的概率，用 Bayes 公式翻一下：

$$P(C_k \mid x_1, \cdots, x_n) = \frac {P(x_1, \cdots, x_n \mid C_k) P(C_k)} {P(x_1, \cdots, x_n)}$$

分母是常数不管。

选取概率最大的 $C_k$ 作为分类的类别 $\hat C$：

$$\hat C = \arg \max_{C_k} P(C_k) P(x_1, \cdots, x_n \mid C_k)$$

为了计算方便，我们非常 naive 地假设 $x$ 之间**条件独立**：

$$P(x_1, \cdots, x_n \mid C_k) = \prod_i P(x_i \mid C_k)$$

代入：

$$\boxed{
    \hat C = \arg \max_{C_k} P(C_k) \prod_{i=1}^n P(x_i \mid C_k)
}$$

## Laplace 平滑系数

https://en.wikipedia.org/wiki/Additive_smoothing

这个模型看起来数学上不错，但是 $P(x_i \mid C_k) = 0$ 怎么办？

TODO:

