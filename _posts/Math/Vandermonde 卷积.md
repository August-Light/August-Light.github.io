# Vandermonde 卷积

$$\boxed{
    \sum_{i=0}^k \binom n i \binom m {k-i} = \binom {n+m} k
}$$

最核心的是这样的结构：

$$\sum_{i=0}^k \binom \square i \binom \square {k-i}$$

- 下指标之和恒定。
- $i$ 遍历全部 $0$ 到下指标之和之间的数。

## 证明

组合意义：从 $n+m$ 个数取 $k$ 个，相当于从 $n$ 个数取 $i$ 个再从 $m$ 个数取 $k-i$ 个，枚举所有的 $i$ 即可遍历所有方案。

OGF 证明：

$$\begin{aligned}
    & \sum_{i=0}^k \binom n i \binom m {k-i} \\
    =& \sum_{i=0}^k [x^i](1+x)^n \times [x^{k-i}](1+x)^m \\
    =& [x^k] ((1+x)^n \times (1+x)^m) \\
    =& [x^k] (1+x)^{n+m} \\
    =& \binom {n+m} k \\
\end{aligned}$$

## 常见技巧

**下指标之差恒定**：利用 $\binom n m = \binom n {n-m}$，具体翻哪个组合数取决于求和范围。例：

$$\begin{aligned}
    & \sum_{i=0}^m \binom n i \binom m i \\
    =& \sum_{i=0}^m \binom n i \binom m {m-i} \\
    =& \binom {n+m} m \\
\end{aligned}$$

$$\begin{aligned}
    & \sum_{i=1}^n \binom n i \binom n {i-1} \\
    =& \sum_{i=0}^{n-1} \binom n {i+1} \binom n i \\
    =& \sum_{i=0}^{n-1} \binom n {n-1-i} \binom n i \\
    =& \binom {2n} {n-1} \\
\end{aligned}$$