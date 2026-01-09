线性代数版本更新！加入了长度、角度、正交等 DLC。

# Projection & Dot Product

由于这一段在开 DLC，所以推导是不严格的，都只是灵感而已。这一段我觉得理应有更高妙的写法，但是我先抄 [3B1B 的答案](https://www.bilibili.com/video/av6299284/)过来吧。

> **欧氏平面**中有一个单位向量 $\hat u$，以它为基础画一个数轴。对于任意一个点 / 向量 $\vec v$，我想知道它投影到数轴上是几，记为 $\text{proj}_{\hat u}(\vec v)$。
>
> <img src=https://cdn.luogu.com.cn/upload/image_hosting/a1heodze.png width=450/>

设

$$\vec v = \begin{bmatrix} x \\ y \end{bmatrix}$$

首先检验一下 $\text{proj}_{\hat u}$ **满足线性性**，它应该是一个线性变换。我们尝试用一个矩阵来描述它。这是一个从向量到标量的变换，应该是一个 $1 \times 2$ 矩阵。我们设它的元素为 $a, b$。

$$\begin{bmatrix} a & b \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}$$

$a,b$ 应该是原来的两个标准基向量在投影后的结果：

$$\begin{cases}
    a = \begin{bmatrix} a & b \end{bmatrix} \begin{bmatrix} 1 \\ 0 \end{bmatrix} \\
    b = \begin{bmatrix} a & b \end{bmatrix} \begin{bmatrix} 0 \\ 1 \end{bmatrix} \\
\end{cases}$$

几何意义如下：

<img src=https://cdn.luogu.com.cn/upload/image_hosting/8t2eht3d.png width=250/>

$\hat i$ 往 $\hat u$ 投影的长度是多大？若你能意识到 $\hat i$ 与 $\hat u$ 都是单位向量，它们的**投影应该是对称**的，$\text{proj}_{\hat u} (\hat i) = \text{proj}_{\hat i} (\hat u)$。而这实际上就是 $\hat u$ 的 $x$ 分量，$a = \hat u_x$。同理 $b = \hat u_y$。

$$\begin{bmatrix} \hat u_x & \hat u_y \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \hat u_x x + \hat u_y y$$

我们把这个结果称为 $\hat u$ 与 $\vec v$ 的点积。

进一步扩展，当 $\vec u$ 不是单位向量时，我们找到它这个方向上的单位向量 $\hat u$，$\vec u = \lVert \vec u \rVert \hat u$，先把 $\hat u$ 和 $\vec v$ 作点积，然后拉长 $\lVert \vec u \rVert$ 倍。最后的结果即为

$$\begin{bmatrix} u_x & u_y \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = u_x x + u_y y$$

我们发现点积就是每一维乘起来然后加起来。那我们终于可以写出一个严谨的定义：

【定义】$n$ 维向量 $\vec a, \vec b$ 的**点积 (inner product)** 定义为

$$\boxed{
    \langle \vec a, \vec b \rangle = \vec a \cdot \vec b
    = \begin{bmatrix} a_1 \\ \vdots \\ a_n \end{bmatrix} \cdot \begin{bmatrix} b_1 \\ \vdots \\ b_n \end{bmatrix}
    := \vec a^T \vec b = \begin{bmatrix} a_1 & \cdots & a_n \end{bmatrix} \begin{bmatrix} b_1 \\ \vdots \\ b_n \end{bmatrix}
    = \sum_{i=1}^n a_i b_i
}$$

点积具有**交换律**：$\vec a \cdot \vec b = \vec b \cdot \vec a$。可以理解为，我们先对 $\hat a$ 和 $\hat b$ 这两个对称的单位向量做了点积，然后乘上 $\lVert \vec a \rVert \lVert \vec b \rVert$ 的倍数。

点积具有**双线性性**：它对 $\vec u, \vec v$ 都是线性的。

刚才的标量投影可以这么定义：

$$\boxed{
    \text{proj}_{\vec u} (\vec v) := \frac {\langle \vec u, \vec v \rangle} {\lVert \vec u \rVert}
}$$

## Orthogonal

按照**欧氏几何**的朴素思路，若 $\vec u$ 到 $\vec v$ 的投影是 $0$ 向量，则 $\vec u \perp \vec v$。

【定义】$\vec u$ **正交 (orthogonal)** 于 $\vec v$，当且仅当 $\langle \vec u, \vec v \rangle = 0$：

$$\vec u \perp \vec v \iff \langle \vec u, \vec v \rangle = 0$$

## Length & Angle

有了点积之后，“软软的”线性空间变得“硬邦邦”了。比如长度可以定义了：

$$\boxed{
    \lVert \vec x \rVert := \sqrt{\langle \vec x, \vec x \rangle}
}$$

单位向量可以这么写：

$$\boxed{
    \hat x = \frac {\vec x} {\lVert \vec x \rVert}
}$$

同时，根据欧式几何的知识，我们知道 $\hat a, \hat b$ 的点积即为它们夹角 $\theta$ 的余弦值 $\cos \theta$：

$$\boxed{
    \theta_{\vec a, \vec b} := \arccos \frac {\vec a \cdot \vec b} {\lVert \vec a \rVert \lVert \vec b \rVert}
}$$

# Least Square Method

> 生活中，我们遇到了一个方程
>
> $$\mathbf A \vec x = \vec b$$
>
> 但是非常遗憾，由于测量误差或随机性等原因，这个方程无解，即 $\vec b \not \in C(\mathbf A)$。
>
> 但是还是得解啊，怎么办？

我们可以尝试求出 $\vec b$ 到 $C(\mathbf A)$ 的投影。或者说，从 $\vec b$ 作一条垂线到 $C(\mathbf A)$ 看垂足。

用什么方法可以刻画这一点？

Method 1

$$\vec b - \mathbf A \vec x \perp C(\mathbf A)$$

老样子，拆包 $\mathbf A = \begin{bmatrix} \vec a_1 & \cdots & \vec a_n \end{bmatrix}$，那么

$$\vec b - \mathbf A \vec x \perp \vec a_i$$

$$\langle \vec a_i, \vec b - \mathbf A \vec x \rangle = 0$$

$$\vec a_i^T (\vec b - \mathbf A \vec x) = 0$$

我们再打包回去：

$$\begin{bmatrix} a_1^T \\ \vdots \\ a_n^T \end{bmatrix} (\vec b - \mathbf A \vec x) = 0$$

$$\mathbf A^T (\vec b - \mathbf A \vec x) = 0$$

但是别急，回到前一步，我们可以得到这个结论：

$$\boxed{
    \vec b - \mathbf A \vec x \in N(\mathbf A^T)
}$$

而我们又知道 $\vec b - \mathbf A \vec x \perp C(\mathbf A)$。

$C(\mathbf A) \perp N(\mathbf A^T)$

---

Method 2 在 $C(\mathbf A)$ 里找一个 $\mathbf A \vec x^*$，到 $\vec b$ 距离最短。

$$\arg \min_{\vec x^*} \lVert \vec b - \mathbf A \vec x^* \rVert$$


## Normal Equation

回到这一步：

$$\mathbf A^T (\vec b - \mathbf A \vec x) = 0$$

再推一步就得到了**正规方程 (Normal Equation)**：

$$\boxed{
    \mathbf A^T \mathbf A \vec x = \mathbf A^T \vec b
}$$

若 $\mathbf A^T \mathbf A$ 可逆，则我们就解出来了：

$$\boxed{
    \vec x = (\mathbf A^T \mathbf A)^{-1} \mathbf A^T \vec b
}$$

# Fundamental Theorem of Linear Algebra

<img src=https://cdn.luogu.com.cn/upload/image_hosting/otjx50f2.png width=450/>

$C(\mathbf A) \perp N(\mathbf A^T)$

