# 复数

## 模长

$$\lvert \lvert z_1 \rvert - \lvert z_2 \rvert \rvert \le \lvert z_1 + z_2 \rvert \le \lvert z_1 \rvert + \lvert z_2 \rvert$$

## 单位根

$$\prod_{k=0}^{n-1} (z - \omega_n^k) = z^n - 1$$

对于偶数 $n$：

$$\prod_{k \text{ odd}} (z - \omega_n^k) = z^{\frac n 2} + 1$$

# Example 5.21 [AIME II 2008 #13](https://artofproblemsolving.com/wiki/index.php?title=2008_AIME_II_Problems/Problem_13) (Normal)

> 复平面上有一个边长为 $\frac 1 {\sqrt 3}$ 且中心在原点的正六边形，有一组对边与虚轴平行。
>
> 设该六边形以外的区域为 $R$，对 $R$ 中的所有复数作变换 $z \mapsto \frac 1 z$，求 $R$ 变换完后的面积。

由于有对称性，为了方便，我们把变换改为 $z \mapsto \frac 1 {\bar z}$，这样辐角不变。这样容易看出，这个变换此时只和 $\lvert z \rvert$ 有关，也就是说它是各向同性的。

## Sol 1

我们可以把六边形改成 $12$ 个小三角形分别计算面积。

考虑最右边这条边，辐角为 $\theta$ 处的模长为 $\frac 1 2 \sec \theta$，反演后为 $r = 2 \cos \theta$。

$$\begin{aligned}
    & \frac 1 2 \int_0^{\frac \pi 6} r^2 d\theta \\
    =& \frac 1 2 \int_0^{\frac \pi 6} (2 \cos \theta)^2 d\theta \\
    =& 2 \int_0^{\frac \pi 6} \frac {\cos 2 \theta + 1} 2 d\theta \\
    =& \frac \pi 6 + \frac {\sqrt 3} 4 \\
\end{aligned}$$

$$\text{Area} = 12 \times \left( \frac \pi 6 + \frac {\sqrt 3} 4 \right) = \boxed{2 \pi + 3 \sqrt 3}$$

## Sol 2

这个变换等价于关于单位圆的**反演变换**。熟知结论**反演变换保广义圆不变**，直线在反演变换下会变成圆或保持直线。

我们可以直接画出变换后的样子：

<img src="https://cdn.luogu.com.cn/upload/image_hosting/b232jwo2.png" width=500/>

这个图的面积是十分容易计算的，可得 $\boxed{2 \pi + 3 \sqrt 3}$。

# Example 5.19 CHKMO 2021 #4 (Normal)

这个题目好像有高等背景。[A099390](https://oeis.org/A099390)

> 证明：对任意正整数 $n$，$\prod_{k=1}^n (1 + 4 \cos^2 \frac {k \pi} {2n+1})$ 是整数。[A001519](https://oeis.org/A001519)

$$\begin{aligned}
    & \prod_{k=1}^n (1 + 4 \cos^2 \frac {k \pi} {2n+1}) \\
    =& \prod_{k=1}^n \left( 3 + 2 \cos (k \times \frac {2 \pi} {2n+1}) \right) \\
    =& \prod_{k=1}^n (3 + \omega_{2n+1}^k + \omega_{2n+1}^{-k}) \\
    =& \sqrt{ \frac 1 5 \prod_{k=0}^{2n} (3 + \omega_{2n+1}^k + \omega_{2n+1}^{-k})}
\end{aligned}$$

令 $m = 2n+1$：

$$\begin{aligned}
    & \prod_{k=0}^{m-1} (\omega_m^k + 3 + \omega_m^{-k}) \\
    =& \prod_{k=0}^{m-1} (\omega_m^{2k} + 3 \omega_m^k + 1) \\
    =& \prod (\omega_m^k - r_1) (\omega_m^k - r_2) & r_{1,2} = \frac {- 3 \pm \sqrt 5} 2 \\
    =& (r_1^m - 1) (r_2^m - 1) \\
    =& 2 - r_1^m - r_2^m & r_1 r_2 = 1 \\
    =& 2 + (-r_1)^m + (-r_2)^m \\
\end{aligned}$$

现在只要证明它永远是整数：

$$\sqrt{\frac {2 + (-r_1)^m + (-r_2)^m} 5}$$

注意到

$$\frac {3 \pm \sqrt 5} 2 = \left( \frac {1 \pm \sqrt 5} 2 \right)^2$$

设 $\varphi = \frac {1 + \sqrt 5} 2, \psi = \frac {1 - \sqrt 5} 2$，$F$ 为 Fibonacci 数：

$$\begin{aligned}
    & \sqrt{\frac {2 + (-r_1)^m + (-r_2)^m} 5} \\
    =& \frac 1 {\sqrt 5} \sqrt{2 + \varphi^{2m} + \psi^{2m}} \\
    =& \frac 1 {\sqrt 5} (\varphi^m + \psi^m) \\
    =& F_m = \boxed{F_{2n+1}}
\end{aligned}$$

