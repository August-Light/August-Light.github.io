---
title: 'Tongrui 1 几何 Part 1【施工中】'
date: 2026-01-30
permalink: /posts/2026/01/2026-01-30-Tongrui-1-几何-Part-1/
excerpt: "这么难？？"
tags:
  - Math
---

这一段部分题目比较水或者只需要特定的观察，因此只记有价值 / 有借鉴意义的部分。

# 公式 / 模型

## 垂心与外接圆

练习题：Example 1.16 [AIME I 2020 #15](https://artofproblemsolving.com/wiki/index.php?title=2020_AIME_I_Problems/Problem_15)

**三角形垂心关于边的对称点在外接圆上**。证法是 $\angle BAC + \angle BHC = \pi$。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/qhiuytey.png" width=400>

## Stewart 定理

> 根据 $b,c,m,n$，求出 $d$：
>
> <img src="https://cdn.luogu.com.cn/upload/image_hosting/j0ibegeu.png" width=450/>

在点 $B$ 处放一个质量为 $n$ 的质点，在点 $C$ 处放一个质量为 $m$ 的质点。可以发现这个质点系的质心在 $D$。

写出该质点系对质心的转动惯量：

$$I_{CM} = m n^2 + m^2 n = mn(n+m)$$

写出该质点系对 $A$ 的转动惯量：

$$I = b^2 m + c^2 n$$

对这两个转动惯量使用平行轴定理：

$$I = I_{CM} + (m+n) d^2$$

$$\boxed{
    b^2 m + c^2 n = (m+n) (d^2 + mn)
}$$

进一步思考，甚至可以得到 **Stewart 定理与质点系的平行轴定理等价**。对一个 $n$ 个点的质点系进行归纳，先把前 $n-1$ 个质点的质量等效在质心，将这个质心与第 $n$ 个质点使用 Stewart 定理即可。

## 重心到三角形顶点距离平方和

练习题：Example 5.22 [AIME I 2012 #14](https://artofproblemsolving.com/wiki/index.php?title=2012_AIME_I_Problems/Problem_14)

在三角形 $ABC$ 中，重心为 $G$，则：

$$\boxed{
    GA^2 + GB^2 + GC^2 = \frac 1 3 (a^2 + b^2 + c^2)
}$$

对于一个任意点 $P$：

$$\boxed{
    PA^2 + PB^2 + PC^2 \ge \frac 1 3 (a^2 + b^2 + c^2)
}$$

取等当且仅当 $P$ 是重心 $G$。

## 证明

在 $A,B,C$ 处各放置一个质量为 $1$ 的质点。

计算质心 $G$ 处转动惯量：

$$I_G = GA^2 + GB^2 + GC^2$$

使用三次平行轴定理：

$$\begin{cases}
    I_A = I_G + 3 GA^2 = b^2 + c^2 \\
    I_B = I_G + 3 GB^2 = a^2 + c^2 \\
    I_C = I_G + 3 GC^2 = a^2 + b^2 \\
\end{cases}$$

$$\begin{aligned}
    6 (GA^2 + GB^2 + GC^2) &= 2 (a^2 + b^2 + c^2) \\
    GA^2 + GB^2 + GC^2 &= \frac 1 3 (a^2 + b^2 + c^2)
\end{aligned}$$

得证。

进一步地，对于任意一点 $P$，有

$$PA^2 + PB^2 + PC^2 = I_P = I_G + 3 PG^2 \ge I_G$$

取等当且仅当 $PG = 0$，即 $P$ 就是 $G$。

## Euler 定理与 Euler 不等式

练习题：Example 1.9 [AIME II 2024 #10](https://artofproblemsolving.com/wiki/index.php?title=2024_AIME_II_Problems/Problem_10)

> 三角形 $ABC$ 中，内心为 $I$，外心为 $O$，内切圆、外接圆半径为 $r,R$。
>
> 证明：**两心之间的距离 $OI$ 只由 $R,r$ 决定**，并求出具体表达式。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/t2ooe1qp.png" width=400>

求 $OI$ 等价于求 $I$ 对圆 $O$ 的幂。为了使用圆幂，我们要在图中找一条合适的过 $I$ 的弦。对于内心 $I$ 来说，最合适的肯定就是它和一个顶点的的连线。

$$\Pi_O(I) = OI^2 - R^2 = - AI \times IP$$

根据鸡爪定理，$IP = BP$。接下来我们只要把 $AI \times BP$ 表示成 $R,r$ 的形式即可。

构造图中这对蓝色相似三角形，得：

$$\begin{aligned}
    \frac r {BP} &= \frac {AI} {2R} \\
    AI \times BP &= 2Rr \\
    AI \times IP &= 2Rr \\
    OI^2 - R^2 &= -2Rr \\
\end{aligned}$$

最终得到

$$\Pi_O(I) = OI^2 - R^2 = - 2Rr$$

$$\boxed{
    OI^2 = R (R - 2r)
}$$

推论（**Euler 不等式**）：

$$\boxed{
    R \ge 2r
}$$

取等条件为 $OI = 0$，即三角形为等边三角形。

## 反演变换

TODO:

## Ptolemy 定理

TODO:

不等式

## 角元 Menelaus 与 Ceva 定理

TODO:

## 类似中线

https://zhuanlan.zhihu.com/p/718821665

https://zhuanlan.zhihu.com/p/407949882

https://artofproblemsolving.com/wiki/index.php/Symmedians,_Lemoine_point?srsltid=AfmBOopx8IQ30O_iBz0GgDM5OzFk3waJO5dYipToSf5yJ00L8dV6YmaH

[BMO2 2024 #3](https://bmos.ukmt.org.uk/home/bmo2-2024.pdf)

https://bmos.ukmt.org.uk/solutions/bmo2-2024/


TODO:

# Example 1.5 [AIME II 2002 #14](https://artofproblemsolving.com/wiki/index.php?title=2002_AIME_II_Problems/Problem_14) (Normal)

暴算勾股定理太困难，改用三角函数，将勾股定理完全打包在三角函数的内在性质中。

类似题目：Example 1.19

> 直角三角形 $APM$ 中，$A$ 是直角，周长为 $152$。在边 $AP$ 上取一点 $O$ 为圆心画一个半径为 $19$ 的圆，正好和 $AM$ 与 $PM$ 都相切。求 $OP$。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/065y2l7x.png" width=400/>

拿到题目的第一反应是用勾股定理列一堆方程开始硬解，显然非常麻烦！我们可以用**三角函数**来刻画这个问题。

$$19 (1 + 2 \cot \theta + \tan 2 \theta + \sec 2 \theta) = 152$$

$$2 \cot \theta + \tan 2 \theta + \sec 2 \theta = 7$$

同时出现 $\theta$ 和 $2 \theta$，**万能公式**是一个不错的选择。

设 $t = \tan \theta$，有 $\tan 2 \theta = \frac {2t} {1 - t^2}$，$\sec 2 \theta = \frac {1 + t^2} {1 - t^2}$。

$$\frac 2 t + \frac {2t} {1 - t^2} + \frac {1 + t^2} {1 - t^2} = 7$$

解出 $t = \frac 1 2$，$\sec 2 \theta = \frac 5 3$。答案为 $19 \times \frac 5 3 = \boxed{\frac {95} 3}$。

# Example 1.8 [AIME II 2020 #13](https://artofproblemsolving.com/wiki/index.php?title=2020_AIME_I_Problems/Problem_13)

TODO:



# Example 1.11 [AIME I 2023 #12](https://artofproblemsolving.com/wiki/index.php?title=2023_AIME_I_Problems/Problem_12) (Normal)

Solution 3 的解法

TODO:

结论：在**等边三角形**中，

- 三条红线之和为定值，为一条高的长度。
- 三条绿线之和等于三条蓝线之和为定值，为半周长。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/ljlzv2ds.png" width=400/>

TODO:

# Example 1.12 [AIME II 2021 #14](https://artofproblemsolving.com/wiki/index.php?title=2021_AIME_II_Problems/Problem_14)

TODO: Simson 线

# Example 1.14 (Normal)

TODO:

# Example 1.15 [AIME I 2016 #15](https://artofproblemsolving.com/wiki/index.php?title=2016_AIME_I_Problems/Problem_15) (Hard)

神题！几何机械化思考的典范。

> 有两个圆 $\omega_1, \omega_2$ 交于 $X,Y$。作它们的一条公切线，切点为 $A,B$。
>
> 又有一个圆 $\omega_3$，它和 $\omega_1$ 交于 $D$，和 $\omega_2$ 交于 $C$。$D,Y,C$ 恰好三点共线。
>
> 已知 $XC = 67, XD = 37$ 以及 $XY = 47$。
>
> 求 $AB^2$。
>
> <img src="https://cdn.luogu.com.cn/upload/image_hosting/1b0a87ij.png" width=400>

相交圆公切线，辅助线肯定要作它们的公共弦（根轴），延长公共弦与公切线交于 $Z$，有经典结论 $AZ=BZ$。

三个圆的三个根轴交于根心，所以我们延长 $DA, CB, YX$，三线共点交于根心 $P$。

对三角形 $CDP$ 使用 Miquel 定理，得到 $AXBP$ 四点共圆。

对于圆 $AXBP$ 使用圆幂定理，$AZ^2 = ZX \times ZP$。同时我们前面在观察 1 的经典结论中已经知道了 $AZ^2 = ZX \times ZY$，可得 $ZP = ZY$。

由 $ZP=ZY$ 且 $ZA=ZB$ 可得 $AYBP$ 是平行四边形。四点共圆导出相似 $\triangle DXP \sim \triangle PXC$。算出 $PX = \sqrt{37 \times 67}$。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/gnbdwjc7.png" width=400>

此时 $PY$ 上的所有边都能算了。最后可以得到 $AB^2 = 37 \times 67 - 47^2 = \boxed{270}$。

# Example 1.18 [AIME I 2009 #12](https://artofproblemsolving.com/wiki/index.php?title=2009_AIME_I_Problems/Problem_12) (Normal)

TODO:

# Example 1.19 [AIME I 2019 #11](https://artofproblemsolving.com/wiki/index.php?title=2019_AIME_I_Problems/Problem_11) (Hard)

类似题目：Example 1.5

这是我第一次遇到「勾股定理换三角函数」这个 Trick 的题目，大受震撼。

> 有一个三边均为整数的等腰三角形 $ABC$，$A$ 为顶角，内心为 $I$，三个旁心为 $I_A, I_B, I_C$。
>
> 已知存在一个圆的圆心为内心 $I$，与旁切圆 $I_A$ 内切，与旁切圆 $I_B, I_C$ 外切。
>
> 求三角形 $ABC$ 的最小周长。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/v52idrib.png" width=500>

勾股定理太烦，用三角函数做。

根据题目条件：

$$r + 2 r_A = I I_B - r_B$$

令 $a = MC$，$\theta = \angle MCI$。依次求出：

$$\begin{cases}
    r = a \tan \theta \\
    r_A = a \cot \theta \\
    r_B = AM = a \tan 2 \theta \\
    I I_B = IC \sec 2 \theta = a \sec \theta \sec 2 \theta \\
\end{cases}$$

代入并约掉 $a$：

$$\tan \theta + 2 \cot \theta = \sec \theta \sec 2 \theta - \tan 2 \theta$$

解得

$$\sec 2 \theta = 9$$

$$AC = a \sec2 \theta = 9a = \frac 9 2 BC$$

因此最小的情况是 $BC = 2, AC = 9$，答案为 $\boxed{020}$。

## 这个三角方程具体怎么解？

TODO:

# Example 1.20 (Hard)



# Example 1.22 (Hard)


# Example 1.23 (Hard)


Example 1.24