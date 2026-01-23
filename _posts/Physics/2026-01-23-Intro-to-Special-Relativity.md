---
title: 'Intro to Special Relativity'
date: 2026-01-23
permalink: /posts/2026/01/2026-01-23-Intro-to-Special-Relativity/
excerpt: "高二上期末考完啦！"
tags:
---

# 事件与参考系

一个**事件**在参考系 $S$ 中拥有一个确定的**位置** $(x,y,z)$ 和一个确定的**时间** $t$。因此我们可以用一个四维坐标来表示它：

$$(t,x,y,z)$$

如果我换一个参考系 $S'$，则同一个事件在参考系应该有一个新的坐标：

$$(t,x,y,z) \mapsto (t' x', y', z')$$

在不同的**时空观**下，这个变换是不一样的。后文我们将展开研究不同的时空观及其变换。

# Galilean transformation

- [时空 - Wiki](https://zh.wikipedia.org/wiki/%E6%97%B6%E7%A9%BA)
- [伽利略变换 - Wiki](https://zh.wikipedia.org/wiki/%E4%BC%BD%E5%88%A9%E7%95%A5%E5%8F%98%E6%8D%A2)
- [伽利略不变性 - Wiki](https://zh.wikipedia.org/wiki/%E4%BC%BD%E5%88%A9%E7%95%A5%E4%B8%8D%E5%8F%98%E6%80%A7)

我们最朴素的直觉认为，**所有参考系中的时间都应该相同**：

$$t' = t$$

为了简化运算，考虑一个坐标系 $S'$ 相对于 $S$ 往 $x$ 轴正方向以 $v$ 的速度匀速运动（这样不用在意 $y,z$ 方向上的运动），且 $t = t' = 0$ 时两者原点重合：

<img src="https://upload.wikimedia.org/wikipedia/commons/9/90/Standard_conf.png" width=300>

经过了 $t$ 的时间后，每一个事件 $(x,y,z,t)$ 应该只是做一个简单的平移：

$$\boxed{\begin{cases}
    x' = x - vt \\
    y' = y \\
    z' = z \\
    t' = t \\
\end{cases}}$$

这种简单的，符合日常生活直觉的变换被称为 **Galilean transformation**，叫这个名字是因为它符合 Galileo 和 Newton 等人的**绝对时空观**。

我们把空间的每一维对时间求偏导，则可以得到**速度**的变换关系：

$$\boxed{\begin{cases}
    \dot x' = \dot x - v \\
    \dot y' = \dot y \\
    \dot z' = \dot z \\
\end{cases}}$$

# 光速不变

- [Michelson–Morley experiment - Wiki](https://en.wikipedia.org/wiki/Michelson%E2%80%93Morley_experiment)

根据 Maxwell 方程组，我们可以得到电磁波的速度是一个常数（根据现代的知识，我们知道光也是电磁波的一种）：

$$c = \frac 1 {\sqrt{\mu_0 \varepsilon_0}}$$

但是，速度是相对的量，Maxwell 方程组**没有说过这个 $c$ 是相对于谁的**。

于是大家觉得，~~总不可能每一个参考系里光速都相等吧~~，应该是有一个地位特殊的**绝对参考系**。那我们的地球应该相对于这个绝对参考系有一个速度，光速与地球速度一叠加，地球上往各个方向的光应该是速度不同的。我们只要测出地球上各个方向的光速就可以验证一下。

然而很遗憾，Michelson–Morley 实验告诉我们，**地球上各个方向的光速都相同**。排除掉“地球是宇宙中特殊的地方”这种逆天的假说，我们就得到了一个~~还是很逆天的~~理论：

**光速在任何参考系中不变，均为 $c$**。

这样的时空观就是**狭义相对论 (Special Relativity)** 的时空观，其中的时空变换称为 **Lorentz transformation**。

但是这显然和 Galilean transformation 是不符的。这咋办？

# Lorentz transformation 的性质

以下采用 $c=1$ 的**自然单位制**。

## 性质 1：时空间隔为 $0$ 在变换下不变

为了方便，找两个 $t=t'=0$ 的参考系 $S$ 和 $S'$。我在 $t=t'=0$ 时从原点发一束光，这两个参考系中的光速应该相等：

$$\frac {\sqrt{x^2 + y^2 + z^2}} t = \frac {\sqrt{x'^2 + y'^2 + z'^2}} {t'} = 1$$

$$\begin{cases}
    t^2 - x^2 - y^2 - z^2 = 0 \\
    t'^2 - x'^2 - y'^2 - z'^2 = 0 \\
\end{cases}$$

进一步地，其实也不是非得有一束光：

对于一个事件 $(x,y,z,t)$，若它在坐标系 $S$ 满足

$$x^2 + y^2 + z^2 - t^2 = 0$$

则可以导出在坐标系 $S'$ 中

$$x'^2 + y'^2 + z'^2 - t'^2 = 0$$

更进一步地，也不是非得用坐标原点进行讨论：若承认**空间平移不变性**与**时间平移不变性**，对于两个事件 $(x_1, y_1, z_1, t_1)$ 和 $(x_2, y_2, z_2, t_2)$，若

$$(\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2 - (\Delta t)^2 = 0$$

（此处 $\Delta t = t_2 - t_1$，其它以此类推）则变换后依然满足

$$(\Delta x')^2 + (\Delta y')^2 + (\Delta z')^2 - (\Delta t')^2 = 0$$

$$\boxed{\begin{aligned}
    & (\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2 - (\Delta t)^2 = 0 \\ \implies & (\Delta x')^2 + (\Delta y')^2 + (\Delta z')^2 - (\Delta t')^2 = 0 \\
\end{aligned}}$$

## 性质 2：是线性变换

设 $\tilde x = (t,x,y,z)$。我们希望从 $S$ 到 $S'$ 的时空变换 $\tilde x \mapsto f(\tilde x)$ 是一个满足**空间平移不变性**与**时间平移不变性**的变换。

即：存在一个函数 $g$ 使得对于任意 $\tilde x, \tilde a$ 有

$$f(\tilde x + \tilde a) - f(\tilde x) = g(\tilde a)$$

研究一下它的性质。我们考虑连续做两次，即研究 $f(\tilde x + \tilde a + \tilde b)$ 的行为：

$$\begin{aligned}
    & f(\tilde x + \tilde a + \tilde b) \\
    =& f(\tilde x) + g(\tilde a + \tilde b) \\
\end{aligned}$$

$$\begin{aligned}
    & f(\tilde x + \tilde a + \tilde b) \\
    =& f(\tilde x + \tilde a) + g(\tilde b) \\
    =& f(\tilde x) + g(\tilde a) + g(\tilde b)
\end{aligned}$$

$$g(\tilde a) + g(\tilde b) = g(\tilde a + \tilde b)$$

这不是我们的老朋友 **Cauchy 方程**嘛！因此，对于性质良好的 $g$（例如连续），$g$ 是一个线性变换。对于向量来说，其实就是存在一个矩阵 $\Lambda$，使得

$$g(\tilde x) = \Lambda \tilde x$$

进一步地

$$f(\tilde x) = \Lambda \tilde x + f(0)$$

**不妨设 $f(0) = 0$ 保持原点不变**，则 $f$ 是一个**线性变换**：

$$\boxed{
    f(\tilde x) = \Lambda \tilde x
}$$

## 性质 3：不变量

看性质 1 中的这个结构：

$$(\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2 - (\Delta t)^2 = 0$$

线性代数学得比较好的同学应该能意识到，这是一个**二次型**。我们定义**时空间隔** $\Delta s$ 为这个量的平方根：

$$(\Delta s)^2 = (\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2 - (\Delta t)^2$$

若我们定义**度规**

$$\eta = \begin{bmatrix}
    -1 \\
    & 1 \\
    & & 1 \\
    & & & 1 \\
\end{bmatrix}$$

则

$$s^2 = (\Delta \tilde x)^T \eta (\Delta \tilde x)$$

在 $s^2 = 0$ 时可以导出 $s'^2 = 0$，我们把 $s'$ 显式写出来：

$$\begin{aligned}
    (\Lambda \Delta \tilde x)^T \eta (\Lambda \Delta \tilde x) = 0 \\
    (\Delta \tilde x)^T (\Lambda^T \eta \Lambda) (\Delta \tilde x) = 0
\end{aligned}$$

ChatGPT 说有一个定理保证了：若两个（非退化）二次型的零集相同，则这两个二次型成比例。即存在比例系数 $\lambda$ 使得：

$$\lambda \eta = \Lambda^T \eta \Lambda$$

显然这个系数代表了时空在变换中产生的缩放，**不妨直接让 $\lambda = 1$**。

$$\boxed{
    \eta = \Lambda^T \eta \Lambda
}$$

因此，Lorentz transformation 保持度规 $\eta$ 不变。对应地，时空间隔的平方

$$(\Delta s)^2 = (\Delta \tilde x)^T \eta (\Delta \tilde x)$$

在 Lorentz transformation 下是**不变量**。

## 总结

若 $S \mapsto S'$ 的 Lorentz transformation 满足以下前提条件：
- 空间平移不变性
- 时间平移不变性
- 连续性
- 对空间的缩放系数 $\lambda = 1$
- 保持时空原点不变

则：
- 这个映射是线性变换，可以表示为矩阵。
- $(\Delta s)^2 = (\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2 - (\Delta t)^2$ 是变换的不变量。

# Lorentz boost 的表达式

- [简单相对论(一)：究竟什么是不变的？](https://www.bilibili.com/video/BV1sV4y1Y7fX/)

事情似乎越来越复杂了……我们还是只关注 $x$ 轴方向上的运动吧：

<img src="https://upload.wikimedia.org/wikipedia/commons/9/90/Standard_conf.png" width=300>

这种特殊的 Lorentz transformation 称为 **Lorentz boost**。

对于一个事件 $(t,x)$，它的 Lorentz transformation 不变量是：

$$x^2 - t^2 = s^2$$

这是一个双曲线。我们知道双曲线上的点可以用带双曲角参数的双曲旋转表示：

$$\begin{bmatrix} t' \\ x' \end{bmatrix}
 = \begin{bmatrix}
    \cosh \phi & - \sinh \phi \\
    - \sinh \phi & \cosh \phi \\
\end{bmatrix}
\begin{bmatrix} t \\ x \end{bmatrix}$$

我们选一个特殊点解出 $\phi$ 和 $v$ 的关系。

考虑 $S$ 中过了时间 $t$ 后 $S'$ 原点的位置：
- 在 $S$ 的视角下是 $(t, vt)$。
- 在 $S'$ 的视角下是 $(t', 0)$。

$$\begin{aligned}
    vt \cosh \phi - t \sinh \phi &= 0 \\
    \tanh \phi &= v \\
    \phi &= \operatorname{artanh} v \\
\end{aligned}$$

双曲角 $\phi$ 称为**快度 (rapidity)**。有了 $\phi$ 和 $v$ 的关系就可以解出一切了：

$$\begin{cases}
    \cosh^2 \phi - \sinh^2 \phi = 1 \\
    \frac {\sinh \phi} {\cosh \phi} = v
\end{cases}$$

解出

$$\begin{cases}
    \cosh v = \frac 1 {\sqrt{1 - v^2}} \\
    \sinh v = \frac v {\sqrt{1 - v^2}}
\end{cases}$$

令 **Lorentz 因子** $\gamma = \frac 1 {\sqrt{1 - v^2}}$，则 Lorentz boost 的表达式为：

$$\boxed{
    \begin{bmatrix} t' \\ x' \end{bmatrix}
    = \begin{bmatrix}
        \gamma & - \gamma v \\
        - \gamma v & \gamma \\
    \end{bmatrix}
    \begin{bmatrix} t \\ x \end{bmatrix}
}$$

> $S_1$ 相对 $S$ 的速度为 $v_1$，$S_2$ 相对 $S_1$ 的速度为 $v_2$。求 $S_2$ 相对 $S$ 的速度。

连续两次双曲旋转，只要把双曲角相加：

$$\begin{cases}
    \phi_1 = \operatorname{artanh} v_1 \\
    \phi_2 = \operatorname{artanh} v_2 \\
    \phi = \phi_1 + \phi_2 \\
\end{cases}$$

$$\boxed{
    v = \tanh(\operatorname{artanh} v_1 + \operatorname{artanh} v_2) = \frac {v_1 + v_2} {1 + v_1 v_2}
}$$

真正是线性的物理量不是速度，而是快度。

> 怎么理解光速是速度的上限？

切回普通的单位制：

$$\phi = \operatorname{artanh} \frac v c$$

$v \to c$ 时 $\phi \to \infty$。

当 $v=c$ 时 $\phi = \infty$，无穷大加什么都还是无穷大，因此光速在任何参考系中不变。

> 为什么生活中的常识会认为速度是线性的？

求出 $\operatorname{artanh}$ 的 Maclaurin 展开：

$$\operatorname{artanh} x = x + \frac {x^3} 3 + \frac {x^5} 5 + \cdots = \sum_{n=0}^\infty \frac {x^{2n+1}} {2n+1}$$

$$x \to 0, \ \operatorname{artanh} x \sim x$$

（切回普通的单位制）生活中，$\frac v c$ 非常接近 $0$，因此 $\operatorname{artanh} \frac v c \approx \frac v c$，那就是线性的了。