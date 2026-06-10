# 聚类

无监督学习算法。

## 聚类的评估

### SSE (Sum of Squared Errors)

$$SSE = \sum_{i=1}^k \sum_{j \in C_k} \lVert x_j - \mu_i \rVert^2$$

$SSE$ 越小越好。

主要考虑了**簇内聚程度**。

### SC (Silhouette Coefficient)

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

### CHI (Calinski–Harabasz Index)

[Wiki](https://en.wikipedia.org/wiki/Calinski%E2%80%93Harabasz_index)

计算以下值：
- $WCSS$ (Within-Cluster Sum of Squares)：和 $SSE$ 一个意思。
- $BCSS$ (Between-Cluster Sum of Squares)：$BCSS = \sum_{i=1}^k \lvert C_i \rvert \lVert \mu_i - \bar \mu \rVert^2$，即每个中心到总中心的距离平方和（对 cluster 的大小加权）。

根据以下公式计算 CHI：

$$CH = \frac {BCSS} {WCSS} \frac {n-k} {k-1}$$

$CH$ 越大越好。

感性理解：$WCSS$ 越小说明 cluster 越紧密；$BCSS$ 越大说明不同的 cluster 分得越开；$k$ 越小越好。

主要考虑了**簇内聚程度**、**簇间分离程度**、**质心个数**。

## $k$-means clustering

以 SSE 为目标函数。

- 随机选择 $k$ 个样本点作为初始聚类中心。
- 把每个点分给（欧氏距离）最近的中心。
- 对每个 cluster 将中心设置为所有点的重心。
- 返回第二步，直到不再发生变化。

### API

[KMeans — scikit-learn 1.8.0 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)

```py
import matplotlib.pyplot as plt
from sklearn.datasets import make_blobs
from sklearn.cluster import KMeans

# 1 生成模拟数据
X, y_true = make_blobs(
    n_samples=300,
    centers=3,
    cluster_std=0.60,
    random_state=0
)

# 2 训练 KMeans
kmeans = KMeans(n_clusters=3, random_state=0)
kmeans.fit(X)

# 3 预测类别
y_kmeans = kmeans.predict(X)

# 4 获取聚类中心
centers = kmeans.cluster_centers_

# 5 可视化
plt.scatter(X[:, 0], X[:, 1], c=y_kmeans)
plt.scatter(centers[:, 0], centers[:, 1], marker='x', s=200)
plt.title("KMeans Clustering")
plt.show()
```

### 怎么确定 $k$

随着 $k$ 增大，当 cost function 从大幅下降突然变为缓慢下降的点，被认为是最优的 $k$。

这被称为 Elbow method，因为图像看起来像一个手肘。

# Naive Bayes Classifier

> 给定一个样本，输入 features $(x_1, \cdots, x_n)$，分类到 classes $C_1, \cdots, C_m$。

我们可以把问题刻画为：

$$\hat C = \arg \max_{C_k} P(C_k \mid x_1, \cdots, x_n)$$

由于我们是已知 $x_1, \cdots, x_n$ 要求 $C_k$ 的概率，用 Bayes 公式翻一下：

$$P(C_k \mid x_1, \cdots, x_n) = \frac {P(x_1, \cdots, x_n \mid C_k) P(C_k)} {P(x_1, \cdots, x_n)}$$

$$\hat C = \arg \max_{C_k} P(C_k) P(x_1, \cdots, x_n \mid C_k)$$

为了计算方便，我们非常 naive 地假设所有 $x$ **条件独立**：

$$P(x_1, \cdots, x_n \mid C_k) = \prod_i P(x_i \mid C_k)$$

代入：

$$\boxed{
    \hat C = \arg \max_{C_k} P(C_k) \prod_{i=1}^n P(x_i \mid C_k)
}$$

实践中一般取对数。

## [Laplace 平滑系数](https://en.wikipedia.org/wiki/Additive_smoothing)

这个模型看起来数学上不错，但是 $P(x_i \mid C_k) = 0$ 怎么办？

$$\begin{aligned}
    & P(x_i \mid C_k) = \frac {\text{count}(x_i, C_k)} {\sum_j \text{count}(x_j, C_k)} \\
    \xRightarrow{\text{Laplace}} \quad & P(x_i \mid C_k) = \frac {\text{count}(x_i, C_k) + \alpha} {\sum_j \text{count}(x_j, C_k) + n \alpha}
\end{aligned}$$

其中 $\alpha$ 可以取 $1$ 或比较小的数，这样改一下就好了。

# 特征降维

## 低方差过滤

删除所有方差小于一定阈值的 feature。

## 主成分分析 (PCA)

[PCA — scikit-learn 1.8.0 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)

PCA 会选取方差最大的若干个正交方向作投影。

参数 `n_components`：
- 若为整数，代表要保留的主成分个数。
- 若为 $0$ 到 $1$ 之间的浮点数 $p$，代表能解释 $p$ 的比例的方差的特征数量。

## Pearson 相关系数 / Spearman 相关系数

对于 feature $X_i$，令 $H_0$ 为「$X_i$ 与 $Y$ 无关」。作 significance test：通过计算相关系数 $r$（Pearson 相关系数 / Spearman 相关系数）然后求出 $p$ 值。若 fail to reject $H_0$，则剔除该 feature。

统计检验可以直接使用 API：
- [pearsonr — SciPy v1.17.0 Manual](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.pearsonr.html)
- [spearmanr — SciPy v1.17.0 Manual](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.spearmanr.html)