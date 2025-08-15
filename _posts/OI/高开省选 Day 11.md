$\text{lcm}$ 卷积也有积性。

$\varphi * 1 = \text{Id}$ 的双射证明 TODO:

# 莫比乌斯反演 例题

## [P5518 [MtOI2019] 幽灵乐团 / 莫比乌斯反演基础练习题](https://www.luogu.com.cn/problem/P5518)

平凡。TODO:

## [P5176 公约数](https://www.luogu.com.cn/problem/P5176) (Easy)

容易注意到分母和前面两项可以消。

答案即为

$$\sum\limits_{i,j,k} \gcd(i,j)^2 + \gcd(j,k)^2 + \gcd(k,i)^2$$

btw 上面这个式子如果不是 $2$ 次方是 $k$ 次方也能做，[P4449 于神之怒加强版](https://www.luogu.com.cn/problem/P4449)

## [P1587 [NOI2016] 循环之美](https://www.luogu.com.cn/problem/P1587)

题目要求：

$$\sum\limits_{i=1}^n \sum\limits_{j=1}^m [i \perp j] [j \perp k]$$

TODO:

## [P5071 [Ynoi Easy Round 2015] 此时此刻的光辉](https://www.luogu.com.cn/problem/P5071)

PR 分解每个数。

直接莫队是 $O(n \sqrt m \log V)$ 的，考虑优化。

根号分治，对小质因子（$\le B$）直接前缀和。

时间复杂度 $O(\pi(B) (n+m) + n \sqrt m \log_B V) = O((n + m) \frac B {\ln B} + n \sqrt m \ln V \frac 1 {\ln B})$，取 $B = \Theta(\frac {n \sqrt m \ln V} {n + m})$ 最优。

## [CF1106F Lunar New Year and a Recursive Sequence](https://www.luogu.com.cn/problem/CF1106F)

简单题 TODO:

## [P4607 [SDOI2018] 反回文串](https://www.luogu.com.cn/problem/P4607)

TODO:

## [P3327 [SDOI2015] 约数个数和](https://www.luogu.com.cn/problem/P3327)

TODO: 经典老题

$$d(ij) = \sum\limits_{x|i} \sum\limits_{y|j} [x \perp y]$$

## [CF1139D Steps to One](https://www.luogu.com.cn/problem/CF1139D)

TODO: 这题有点意思，回顾一下

## [CF1687E Become Big For Me](https://www.luogu.com.cn/problem/CF1687E)

TODO:

## [P4139 上帝与集合的正确用法](https://www.luogu.com.cn/problem/P4139) (Easy)

不写了。

## [P4240 毒瘤之神的考验](https://www.luogu.com.cn/problem/P4240)

$$\varphi(ij) = \dfrac {\varphi(i) \varphi(j) \gcd(i,j)} {\gcd(\varphi(i,j))}$$

