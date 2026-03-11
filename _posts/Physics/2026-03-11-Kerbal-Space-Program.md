---
title: 'Kerbal Space Program'
date: 2026-03-11
permalink: /posts/2026/03/2026-03-11-Kerbal-Space-Program/
excerpt: "坎！"
tags:
---

# 相关网站

- [Kerbal Space Program](https://www.kerbalspaceprogram.com/)
- [Kerbal Space Program Wiki](https://wiki.kerbalspaceprogram.com/wiki/Main_Page)
- [Kerbal Space Program - 灰机wiki](https://ksp.huijiwiki.com/wiki/%E9%A6%96%E9%A1%B5)

# $\Delta v$

https://en.wikipedia.org/wiki/Delta-v

$\Delta v$ 是一段时间内加速度 magnitude 的总和：

$$\Delta v := \int \lvert \dot v \rvert dt$$

对于同样的运动，不同的航天器需要不同量的燃料，但是所需的 $\Delta v$ 是相同的。

# Oberth 效应

https://en.wikipedia.org/wiki/Oberth_effect

对于一个给定的 $\Delta v$，在近日点使用才能使航天器获得最多的能量。

## 推导

$$\begin{aligned}
    \Delta \text{KE} &= \frac 1 2 m \left( (v + \Delta v)^2 - v^2 \right) \\
    &= m v \Delta v + \frac 1 2 m (\Delta v)^2
\end{aligned}$$

$\Delta v$ 不变，$v$ 越大时 $\text{KE}$ 变化越大。而近日点是能量最大的位置。

# Tsiolkovsky 火箭方程

https://en.wikipedia.org/wiki/Tsiolkovsky_rocket_equation

消耗燃料可以获得多少 $\Delta v$？

Tsiolkovsky 火箭方程告诉我们：令 $v_e$ 是相对于火箭的喷气速度，燃料燃烧的过程使火箭质量由 $m_0$ 下降到 $m_f$，则获得的 $\Delta v$ 为：

$$\Delta v = v_e \ln \frac {m_0} {m_f}$$

## 推导

$dm$ 是火箭质量的减少（因此是负数），

$$\begin{aligned}
    mv &= (m + dm) (v + dv) + dm (v_e - v) \\
    &= mv + m dv + v dm + v_e dm - v dm \\
\end{aligned}$$

$$\begin{aligned}
    m dv &= - v_e dm \\
    dv &= - v_e \frac 1 m dm \\
    \int_0^{\Delta v} dv &= - v_e \int_{m_0}^{m_f} \frac 1 m dm \\
    \Delta v &= v_e \ln \frac {m_0} {m_f}
\end{aligned}$$

# Kepler 第三定律

https://en.wikipedia.org/wiki/Kepler%27s_laws_of_planetary_motion

对于一个指定的恒星，绕着它转的所有物体的周期 $T$ 和轨道半长轴 $a$ 的关系为：

$$T^2 \propto a^3$$

具体比例系数：

$$T^2 = \frac {4 \pi^2} {GM} a^3$$

# *Vis-viva* equation

https://en.wikipedia.org/wiki/Vis-viva_equation

对于椭圆轨道：

$$E = - \frac {G M m} {2 a}$$

对于椭圆轨道上任意一处：

$$v = \sqrt{GM \left( \frac 2 r - \frac 1 a \right)}$$

## 推导

设出离心率 $e$，求出近日点与远日点位置：

$$\begin{cases}
    r_p = (1 - e) a \\
    r_a = (1 + e) a \\
\end{cases}$$

设出总机械能 $E$，根据势能求出动能：

$$\begin{cases}
    U_p = - \frac {G M m} {(1 - e) a} \\
    U_a = - \frac {G M m} {(1 + e) a} \\
\end{cases} \implies \begin{cases}
    \frac 1 2 m v_p^2 = E + \frac {G M m} {(1 - e) a} \\
    \frac 1 2 m v_a^2 = E + \frac {G M m} {(1 + e) a}
\end{cases}$$

角动量守恒：

$$m r_p v_p = m r_a v_a$$

开始大力硬算机械能：

$$\begin{aligned}
    r_p v_p &= r_a v_a \\
    \frac 1 2 m v_p^2 r_p^2 &= \frac 1 2 m v_a^2 r_a^2 \\
    \left( E + \frac {G M m} {(1 - e) a} \right) (1-e)^2 a^2 &= \left( E + \frac {G M m} {(1 + e) a} \right) (1+e)^2 a^2 \\
    - 4 e E &= \frac {2 G M m e} a \\
    E &= - \frac {G M m} {2a} \\
\end{aligned}$$

机械能有了，每一点的速度很好算：

$$\begin{aligned}
    - \frac {G M m} {2 a} &= \frac 1 2 m v^2 - \frac {G M m} r \\
    v &= \sqrt{GM \left( \frac 2 r - \frac 1 a \right)}
\end{aligned}$$

# Hohmann 转移

https://en.wikipedia.org/wiki/Hohmann_transfer_orbit

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/Hohmann_transfer_orbit.svg/500px-Hohmann_transfer_orbit.svg.png" width=250>

对于关于同一星球的两个**共面**的**圆形**轨道，我们可以通过 Hohmann 转移在两个轨道之间切换。

从绿色圆形轨道开始，瞬间加速一次使得轨道变为黄色椭圆，在运行到远地点时再次瞬间加速进入红色圆形轨道。

当然瞬间加速是不可能实现的，但是加速所需的时间相对于整个转移时间来说几乎可以忽略不计。

> 转移所需的时间是多长？

我们通过 Kepler 第三定律可以计算出黄色椭圆的周期及转移时间：

$$T = \frac {2 \pi} {\sqrt{GM}} \left( \frac {r_1 + r_2} 2 \right)^{\frac 3 2}$$

注意实际转移时我们只需要走完半个椭圆，因此转移时间为 $\frac T 2$：

$$\frac T 2 = \frac \pi {\sqrt{GM}} \left( \frac {r_1 + r_2} 2 \right)^{\frac 3 2}$$

> 假设第一次加速完后我的速度变成了 $v_f$。$v_f$ 取多少可以恰好上到红色轨道？

直接代入 *Vis-viva* equation：

$$v_f = \sqrt{GM \left( \frac 2 {r_1} - \frac 2 {r_1 + r_2} \right)}$$

> 有时我们不仅想转移到更高轨道，还可能想追上轨道上的某个物体，比如空间站。何时进行第一次加速？

利用 Kepler 第三定律，把 $T$ 用 $T_2$ 表示：

$$\begin{aligned}
    \frac {r_2^3} {T_2^2} &= \frac {(\frac {r_1 + r_2} 2)^3} {T^2} \\
    T &= T_2 \left( \frac {r_1 + r_2} {2 r_2} \right)^{\frac 3 2}
\end{aligned}$$

计算出第一次加速时两物体的相位角，即目标领先我们的角度：

$$\begin{aligned}
    \Delta \theta &= \pi - \omega_2 \times \frac T 2 \\
    &= \pi - \frac {2 \pi} {T_2} \times \frac 1 2 T_2 \left( \frac {r_1 + r_2} {2 r_2} \right)^{\frac 3 2} \\
    &= \pi \left( 1 - \left( \frac {r_1 + r_2} {2 r_2} \right)^{\frac 3 2} \right) \\
\end{aligned}$$

如果错过了这个转移窗口，则需要再等 $\frac {2 \pi} {\lvert \Delta \omega \rvert}$ 的时间。