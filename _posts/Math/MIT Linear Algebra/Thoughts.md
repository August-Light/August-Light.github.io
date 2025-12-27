# 特征值的性质

$$\begin{aligned}
    & \mathbf A^n \vec x \\
    =& \mathbf A^{n-1} (\mathbf A \vec x) \\
    =& \mathbf A^{n-1} \lambda \vec x \\
    =& \cdots \\
    =& \lambda^n \vec x \\
\end{aligned}$$

- $\mathbf A$ 的特征向量一定是 $\mathbf A^n$ 的特征向量；
- $\mathbf A$ 的特征值的 $n$ 次方一定是 $\mathbf A^n$ 的特征值。

# 相似

先看一个奇怪的题：

> $f(x) = 2 x^2 - 1$，$\lvert x \rvert < 1$。求出 $f^{(n)}(x)$ 的公式，这里表示 $f$ 迭代 $n$ 次。
>
> 提示：$f$ 是 Chebyshev 多项式，考虑构造 $2 \cos^2 \theta - 1 = \cos 2 \theta$。

我们换元 $x = \cos \theta$。

$$\begin{aligned}
    f(x) &= f(\cos \theta) \\
    &= 2 \cos^2 \theta - 1 \\
    &= \cos 2 \theta \\
\end{aligned}$$

$$f(\cos \theta) = \cos 2 \theta$$

$f$ 把 $\cos \theta \mapsto \cos 2 \theta$。我们考虑多迭代几次：

$$f^{(2)}(\cos \theta) = f(\cos 2 \theta) = \cos 4 \theta$$

$$f^{(n)} (\cos \theta) = \cos 2^n \theta$$

因此我们得到了结果：

$$f^{(n)}(x) = \cos (2^n \arccos x)$$

---

考虑一下这个做法的本质是什么：
- 把 $x \xrightarrow{\arccos} \theta$；
- 在 $\theta$ 的视角下，$f$ 就只是简单的翻倍，可以轻易计算迭代；
- 最后再 $\theta \xrightarrow{\cos} x$。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/hb1osuc5.png" width=250>

我们设第一步中的 $\arccos$ 为函数 $\varphi$（称为**桥函数**），翻倍 $\theta \mapsto 2 \theta$ 为函数 $g$。

若我们能构造出

$$f(x) = \varphi^{-1}(g(\varphi(x)))$$

则

$$f^{(n)}(x) = \varphi^{-1}(g^{(n)}(\varphi(x)))$$

这套方法被称为**桥函数法**。这套方法能生效，当且仅当 $g^{(n)}$ 可以方便计算。

若函数 $f,g$ 可以通过某个桥函数 $\varphi$ 联系起来，我们就称 $f,g$ **相似**。