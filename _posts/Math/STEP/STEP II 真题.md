# 2019

标答一处错误：第 $3$ 题 (ii) 问的答案应为 $x = -1$。

## 1

重根的一个例题。

> 【引理 1】令 $f(x) = (x - p) g(x)$。$y = f(x)$ 在 $x = a$ 处（$a \ne p$）的切线过 $(p, 0)$ **当且仅当** $g'(a) = 0$。

> 曲线 $C$ 的方程为 $y = A (x-p) (x-q) (x-r)$，其中 $A \ne 0$ 且 $p < q < r$。
>
> 【引理 2】若 $C$ 在 $x = a$ 处（$a \ne p$）的切线过 $(p, 0)$，则 $2a = q + r$ 且切线斜率为 $- \frac 1 4 A (r - q)^2$。
>
> 已知 $C$ 在 $x = a$ 处（$a \ne p$）的切线过 $(p, 0)$，在 $x = c$ 处（$c \ne r$）的切线过 $(r, 0)$。
>
> 证明两条切线平行**当且仅当** $C$ 在 $x = q$ 处的切线与 $C$ 没有其他交点。

切线斜率相等的充要条件：

$$\begin{aligned}
    - \frac 1 4 A (q - p)^2 &= - \frac 1 4 A (r - q)^2 \\
    q - p &= r - q
\end{aligned}$$

这是我们要证明的目标。

$x = q$ 处的导数与切线：

$$y' \vert_{x=q} = A (q - p) (q - r)$$

$$y = A (q - p) (q - r) (x - q)$$

切线与曲线的交点：

$$A (q - p) (q - r) (x - q) = A (x - p) (x - q) (x - r)$$

### 标答做法

对于 $x \ne q$ 的交点：

$$(q - p) (q - r) = (x - p) (x - r)$$

解得

$$x = p + r - q$$

为了使方程（去重后）只有一个实数解，$q$ 和 $p + r - q$ 这两个解必然要相等。

$$\begin{aligned}
    q &= p + r - q \\
    q - p &= r - q \\
\end{aligned}$$

### 我的做法

已知这个方程有至少二重的根 $x = q$。

若 $x = q$ 恰好是二重根，则必然还有一个另外的实根，即切线与曲线还有另外的交点，矛盾。因此 $x = q$ 必须是三重根。

$$\begin{aligned}
    \left. \frac {d^2} {dx^2} (A (q - p) (q - r) (x - q) - A (x - p) (x - q) (x - r)) \right\vert_{x=q} &= 0 \\
    \left. \frac {d^2} {dx^2} ((x - p) (x - q) (x - r)) \right\vert_{x=q} &= 0 \\
\end{aligned}$$

$$\begin{aligned}
    6q - 2 (p + q + r) &= 0 \\
    q - p &= r - q
\end{aligned}$$

## 5：$f$ 的不动点是 $f \circ f$ 的子集

函数迭代不动点的重要性质：$f$ 的不动点是 $f^{(n)}$ 的不动点的子集，以 $f$ 的不动点为根的多项式是以 $f^{(n)}$ 的不动点为根的的多项式的因式。

> 对于函数 $f(x) = p + (x-p) x$，不难求出其不动点 $x = 1,p$。
>
> 证明 $f(f(x))$ 有除 $x=1,p$ 外的不动点当且仅当 $p < -1$ 或 $p > 3$。

$f(x) = x$ 的解必然是 $f(f(x)) = x$ 的解。我们已知 $(x-1) (x-p)$ 是 $f(x) - x$ 的因式，因此它也是 $f(f(x)) - x$ 的因式。

暴力算出剩下的因式（可以预见它是一个二次多项式）：

$$\frac {f(f(x)) - x} {(x-1) (x-p)} = x^2 + (1-p) x + 1$$

计算 $\Delta \ge 0$ 可得 $p \le -1$ 或 $p \ge 3$，然后特判 $p = -1$ 和 $p = 3$ 即可。

# 2020

未完工

## 2：一类画图题 先画图再线性变换

> 在第一象限内绘制 $(x-y)^2 = (x+y)^2 - 2^{x+y}$。
>
> 提示：$(u > 0) \land (u^2 - 2^u \ge 0) \iff 2 \le u \le 4$，因此该图像只出现在 $2 \le x + y \le 4$。

$$\begin{cases}
    u = x + y \\
    v = x - y \\
\end{cases} \iff \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix}
    \frac 1 2 & \frac 1 2 \\
    \frac 1 2 & - \frac 1 2 \\
\end{bmatrix} \begin{bmatrix} u \\ v \end{bmatrix}$$

$$v^2 = u^2 - 2^u \implies v = \pm \sqrt{u^2 - 2^u}$$

$\sqrt{u^2 - 2^u}$ 是一个单峰的函数，并且在 $u = 2, 4$ 处切线斜率无穷大。画出来变换回去就行了。

## 7：Möbius 变换

> $z \mapsto \frac 2 {z - 2}$ 将直线 $\Re z = p$（$p \ne 2$）映射到哪个圆？

设 $z \mapsto w = u + iv$，然后找一个关于 $u,v$ 的二次方程。

$$\begin{aligned}
    w &= \frac 2 {z - 2} \\
    z &= \frac 2 w + 2 \\
    &= \frac 2 {u + iv} + 2 & w = u + iv \\
    &= \frac {2 (u - iv)} {u^2 + v^2} + 2 \\
    &= \left( \frac {2 u} {u^2 + v^2} + 2 \right) + i \left( - \frac {2v} {u^2 + v^2} \right)
\end{aligned}$$

$$\begin{aligned}
    \frac {2u} {u^2 + v^2} + 2 &= p \\
    \frac 2 {p-2} u &= u^2 + v^2 \\
    \left( u - \frac 1 {p-2} \right)^2 + v^2 &= \left( \frac 1 {p-2} \right)^2 \\
\end{aligned}$$

# 2021

当成模考做的。

## 6：无穷小量模板题

> 已知 $\frac 1 3 \pi \le \alpha \le \frac 1 2 \pi$，$0 < w < R$。
>
> 已知
>
> $$d = \frac {w (2R + w)} {2 (R - (R + w) \cos \alpha)}$$
>
> $$\sin(\alpha - \theta) = \frac d {R + d} \sin \alpha$$
>
> $$S = 2 (R + d) (\alpha - \theta) + 2 \alpha (w - d)$$

> 已知 $\frac w R \ll 1$。
>
> 证明：
>
> $$\frac d R \ll 1$$
>
> $$\alpha - \theta \ll 1$$
>
> $$\frac S {2 \alpha (R + w)} \approx \left( \frac {\sin \alpha - \alpha \cos \alpha} {\alpha (1 - \cos \alpha)} \right) \frac w R$$

令 $\Delta = \frac w R$。

$$\begin{aligned}
    \frac d R &= \frac {w (2R + w)} {2 R (R - (R + w) \cos \alpha)} \\
    &= \frac {\Delta (2 + \Delta)} {2 (1 - (1 + \Delta) \cos \alpha)} \\
    &= \frac {2 \Delta + \cancel{\Delta^2}} {2 (1 - \cos \alpha) + \cancel{(2 \cos \alpha) \Delta}} \\
    & \sim \frac 1 {1 - \cos \alpha} \Delta \\
\end{aligned}$$

令 $\Delta_1 = \frac d R$。

$$\begin{aligned}
    \alpha - \theta &= \arcsin \left( \frac d {R + d} \sin \alpha \right) \\
    &= \arcsin \left( (\sin \alpha) \frac {\Delta_1} {1 + \cancel {\Delta_1}} \right) \\
    & \sim \arcsin \left( (\sin \alpha) \Delta_1 \right) \\
    & \sim (\sin \alpha) \Delta_1 \\
\end{aligned}$$

有 $\Delta_1 \sim \frac 1 {1 - \cos \alpha} \Delta$。

$$\begin{aligned}
    S &= 2 (R + d) (\alpha - \theta) + 2 \alpha (w - d) \\
    & \sim 2 R (1 + \cancel{\Delta_1}) (\sin \alpha) \Delta_1 + 2 \alpha R (\Delta - \Delta_1) \\
    & \sim 2 R \frac {\sin \alpha} {1 - \cos \alpha} \Delta + 2 \alpha R \frac {\cos \alpha} {1 - \cos \alpha} \Delta \\
    &= 2R \frac {\sin \alpha - \alpha \cos \alpha} {1 - \cos \alpha} \Delta \\
\end{aligned}$$

$$\begin{aligned}
    2 \alpha (R + w) &= 2 R \alpha (1 + \cancel \Delta) \\
    & \sim 2 R \alpha \\
\end{aligned}$$

$$\frac S {2 \alpha (R + w)} \sim \left( \frac {\sin \alpha - \alpha \cos \alpha} {\alpha (1 - \cos \alpha)} \right) \Delta$$

## 10

没有特别需要记录的知识。只是觉得这题的标答做得也太麻烦了！

> 一根竖直平面内的抛物线轨道以 $a$ 的加速度匀加速向 $x$ 轴负方向运动。轨道上有一个小滑块。
>
> 本题全程以轨道为参考系。轨道的解析式为 $ky = x^2$。小滑块一开始处于 $(0,0)$。

> 证明小滑块的坐标 $(x,y)$ 满足
>
> $$\dot x (\ddot x - a) + \dot y (\ddot y + g) = 0$$
>
> 证明以下量是守恒量：
>
> $$\frac 1 2 (\dot x^2 + \dot y^2) - ax + gy$$

受力分析可知，轨道的支持力是

$$m \begin{bmatrix}
    \ddot x - a \\
    \ddot y + g \\
\end{bmatrix}$$

支持力是法向的，应当与切向的速度垂直：

$$m \begin{bmatrix}
    \ddot x - a \\
    \ddot y + g \\
\end{bmatrix} \cdot \begin{bmatrix}
    \dot x \\
    \dot y \\
\end{bmatrix} = 0 \implies \dot x (\ddot x - a) + \dot y (\ddot y + g) = 0$$

---

根据能量守恒定律，动能与重力势能等于总机械能，而总机械能恰好全部由惯性力做功提供：

$$\frac 1 2 m (\dot x^2 + \dot y^2) + mgy = max$$

约去 $m$ 证得题目所给的量恒为 $0$。

> 求出以下量（用 $a,k,g$ 表示）：
> - 小滑块可以到达的最大高度
> - 小滑块达到最快速度时的 $x$
> - 小滑块的最快速度

小滑块到达最高高度时动能为 $0$（利用 $\dot y = 0$ 与抛物线说明 $\dot x = 0$，或者结合惯性力势能说明），势能等于机械能：

$$\begin{aligned}
    mgy &= max \\
    g \times \frac {x^2} k &= ax \\
    x &= \frac {a k} g \implies y = \frac {a^2 k} {g^2}
\end{aligned}$$

另一个情况，小滑块达到最大速度：

$$\begin{aligned}
    \frac 1 2 mv^2 &= max - mgy \\
    \frac 1 2 v^2 &= ax - g \frac {x^2} k \\
    v^2 &= - \frac {2g} k \left( x - \frac {a k} {2 g} \right)^2 + \frac {a^2 k} {2 g} \implies \begin{cases}
        x = \frac {a k} {2 g} \\
        v = a \sqrt{\frac {k} {2 g}} \\
    \end{cases}
\end{aligned} $$

# 2022

未完工

## 1：借助图像

不要贸然使用 $e$ 关于无理性相关的性质！这可能是超纲的。

> 绘制 $y = \frac {e^x} x$ 的图像。

大致特征：在 $(-\infty, 0)$ 从 $0$ 单调递减到 $- \infty$，在 $(0,1)$ 从 $\infty$ 单调递减到 $e$，在 $(1, \infty)$ 单调递增到 $\infty$。

> 证明关于整数 $n,m$ 的方程无 $n \ne m$ 的解：
>
> $$\frac {e^n} n - \frac {e^m} m = 0$$

不妨设 $n < m$。**从图像上看**，若 $\frac {e^n} n = \frac {e^m} m$，那么 $n$ 必须落在 $(0,1)$，因此不是整数。

# 2023

未完工

## 4：根号线性组合的极小多项式

鬼题。

> $(x - \sqrt 2)^2 = 3$，证明 $x^4 - 10x^2 + 1 = 0$。注意这个方程以 $\sqrt 2 + \sqrt 3$ 为根。
>
> 求出以 $\sqrt 2 + \sqrt 3 + \sqrt 5$ 为根的一个 $8$ 次整系数多项式。答案不带括号。
>
> 已知 $a,b,c$ 是 $t^3 - 3t + 1 = 0$ 的三根。求出以 $a + \sqrt 2, b + \sqrt 2, c + \sqrt 2$ 为根的一个 $6$ 次整系数多项式。答案不带括号。

若求出 $x = \sqrt 2 \pm \sqrt 3$ 再代入，那就一定是错失了出题人的提示。考虑直接变形，且避免求出 $x$。

$$\begin{aligned}
    (x - \sqrt 2)^2 &= 3 \\
    x^2 - 2 \sqrt 2 x + 2 &= 3 \\
    x^2 - 2 \sqrt 2 x - 1 &= 0 \\
    (x^2 - 2 \sqrt 2 x - 1) (x^2 + 2 \sqrt 2 x - 1) &= 0 \\
    x^4 - 10 x^2 + 1 &= 0 \\
\end{aligned}$$

---

$$\begin{aligned}
    x &= \sqrt 2 + \sqrt 3 + \sqrt 5 \\
    (x - \sqrt 5)^2 &= (\sqrt 2 + \sqrt 3)^2 \\
    x^2 - 2 \sqrt 5 + 5 &= 5 + 2 \sqrt 6 \\
    TODO:
\end{aligned}$$

# 2024

未完工

## 5：平移消除次高项

如果提前知道这题的系数其实是有特殊性质的，那就真简单了。

> 求出定义在整数上的函数
>
> $$f(n) = n^2 - 2n - 6$$
>
> $$g(n) = n^2 - 4n + 2$$
>
> 值域的交集。

$$\begin{aligned}
    f(n) &= n^2 - 2n - 6 \\
    &= (n-1)^2 - 7 \\
\end{aligned}$$

$$\begin{aligned}
    g(n) &= n^2 - 4n + 2 \\
    &= (n-2)^2 - 2 \\
\end{aligned}$$

$$\begin{aligned}
    s^2 - 7 &= t^2 - 2 \\
    (s - t) (s + t) &= 5
\end{aligned}$$

然后简单了。

这个小题提示我们可以平移函数使得函数结构相同来解决后面的问题。

> 求出定义在整数上的函数
>
> $$f(n) = n^3 - 3n^2 + 7n$$
>
> $$g(n) = n^3 + 4n - 6$$
>
> 值域的交集。
>
> 提示：$\forall p,q \in \mathbb R, p^2 + pq + q^2 \ge 0$。

提示内容明示一个立方差，显然是最后一步分解因式的时候会用的东西。

使用平移消除次高项的技巧：

$$\begin{aligned}
    f(n) &= n^3 - 3n^2 + 7n \\
    &= (n-1)^3 + 4n + 1 & \text{消除 } n^2 \\
    &= (n-1)^3 + \textcolor{lightgreen}{4} (n-1) + 5
\end{aligned}$$

$$g(n) = n^3 + \textcolor{lightgreen}{4}n - 6$$

$$\begin{aligned}
    s^3 + 4s + 5 &= t^3 + 4t - 6 \\
    (s - t) (s^2 + st + t^2 - 4) &= -11 \\
\end{aligned}$$

然后好做了。

# 2025

未完工

## 1：阴间画图

> Show that $(1, −3)$ is a local maximum point on the curve $y = 2 \min(x^2, x^3) −5x$ and find the other three local maxima and minima on this curve. Sketch the curve.

- $x < 1$: $y = 2x^3 - 5x$, $y' = 6x^2-5$, stationary points $(\pm \sqrt{\frac 5 6}. \mp \frac {10} 3 \sqrt{\frac 5 6})$.
- $x \ge 1$: $y = 2x^2 - 5x$, $y' = 4x-5$, stationary point $(\frac 5 4, - \frac {25} 8)$

本题画图的四个 G1：
- G1：$x < 1$
  - $-1 < x < 1$ 范围内 该函数是奇函数，两个 stationary point 要几乎对称
  - 要经过原点
- G1：$x > 1$
  - 抛物线正确标出顶点
- G1：intercept
  - $x = - \sqrt{\frac 5 2}$ 和 $x = \frac 5 2$ 都要标出。
- G1： relative positions for the two local minima
  - $\left( \frac {10} 3 \sqrt{\frac 5 6} \right)^2 = \frac {250} {27}$；$\left( \frac {25} 8 \right)^2 = \frac {625} {64}$；$\frac {250} {27} > \frac {625} {64}$
  - $\implies - \frac {10} 3 \sqrt{\frac 5 6} < - \frac {25} 8$

## 3：非常规比大小

> 已知 $1 < x < 2$，比大小：$x^{x+2}$ 和 $(x+2)^x$。
>
> 提示：$\frac {\ln x} x$ 在 $(0, e)$ 从 $-\infty$ 递增到 $\frac 1 e$，在 $(e, \infty)$ 递减到 $0$。

本质上就是要比较 $\frac {\ln x} x$ 和 $\frac {\ln(x+2)} {x+2}$。注意到在 $1 < x < 2$ 上，前者是递增的，后者是递减的，因此只需检验右端点 $x = 2$ 时（此时 $x+2 = 4$）的表现即可。

$$\frac {\ln x} x < \frac {\ln 2} 2 = \frac {\ln 4} 4 < \frac {\ln(x+2)} {x+2}$$

## 4：普通的的无限求和

> 求
>
> $$\sum_{k=0}^\infty \left\lfloor \frac {x + 2^k} {2^{k+1}} \right\rfloor$$
>
> 提示：$\lfloor \frac x 2 \rfloor + \lfloor \frac {x + 1} 2 \rfloor = \lfloor x \rfloor$。

先求部分和，然后取极限。

$$\begin{aligned}
    S_n &= \sum_{k=0}^n \left\lfloor \frac {x + 2^k} {2^{k+1}} \right\rfloor \\
    &= \sum_{k=0}^n \left\lfloor \frac {\frac x {2^k} + 1} 2 \right\rfloor \\
    &= \sum_{k=0}^n \left( \left\lfloor \frac x {2^k} \right\rfloor - \left\lfloor \frac x {2^{k+1}} \right\rfloor \right) \\
    &= \cdots \text{(Telescoping)} \\
    &= \lfloor x \rfloor - \left\lfloor \frac x {2^{n+1}} \right\rfloor
\end{aligned}$$

$$\begin{aligned}
    \sum_{k=0}^\infty \left\lfloor \frac {x + 2^k} {2^{k+1}} \right\rfloor &= \lim_{n \to \infty} S_n \\
    &= \lfloor x \rfloor - \lim_{n \to \infty} \left\lfloor \frac x {2^{n+1}} \right\rfloor \\
\end{aligned}$$

分类讨论 $x \ge 0$ 和 $x < 0$ 即可。答案为

$$\sum_{k=0}^\infty \left\lfloor \frac {x + 2^k} {2^{k+1}} \right\rfloor = \begin{cases}
    \lfloor x \rfloor & x \ge 0 \\
    \lfloor x \rfloor + 1 & x < 0 \\
\end{cases}$$

## 7：分母是二次函数的积分 - 全面

> $$\ddot x = 2x \dot x$$
>
> 初值 $x(0)=a$，其中 $a > 0$。
>
> - 情景 1：初值 $\dot x(0)=a^2+p^2$，其中 $p>0$。求解微分方程。
> - 情景 2：初值 $\dot x(0)=a^2-q^2$，其中 $q>0$。讨论 $a,q$ 的不同大小情况，求解微分方程。

$$\begin{aligned}
    \int \ddot x dt &= \int 2x \dot x dt \\
    \dot x &= x^2 + C \\
\end{aligned}$$

### 情景 1

代入初值解得 $C = p^2$。

$$\dot x = x^2 + p^2$$

非常简单的 $\arctan$，略。

### 情景 2

代入初值解得 $C = - q^2$。

注意此题积分**不建议使用反双曲函数**，一是 STEP II 好像不包括这个，二是需要分类讨论 $a < q$ 和 $a > q$，且 $a = q$ 也不好处理。

$$\begin{aligned}
    \dot x &= x^2 - q^2 \\
    \int \frac 1 {x^2 - q^2} dx &= \int dt + C \\
    \frac 1 {2q} \int \frac 1 {x - q} - \frac 1 {x + q} dx &= t + C \\
    \frac 1 {2q} \ln \left\lvert \frac {x-q} {x+q} \right\rvert &= t + C \\
    \left\lvert \frac {x-q} {x+q} \right\rvert &= C e^{2qt} \\
    \frac {x-q} {x+q} &= C e^{2qt} \\
\end{aligned}$$

代入初值解得 $C = \frac {a-q} {a+q}$。

$$\begin{aligned}
    \frac {x-q} {x+q} &= \frac {a-q} {a+q} e^{2qt} \\
    (x-q) (a+q) &= (a-q) (x+q) e^{2qt} \\
    ((a + q) - (a - q) e^{2qt}) x &= q(a + q) + q (a - q) e^{2qt} \\
    x &= q \frac {(a + q) + (a - q) e^{2qt}} {(a + q) - (a - q) e^{2qt}} \\
\end{aligned}$$

特别地，当 $a = q$ 时，解为常数函数 $x = a$。