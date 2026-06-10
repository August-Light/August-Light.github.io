---
title: 'AP E&M Chapter 14-16 Part 3: Inductors'
date: 2025-06-01
permalink: /posts/2025/06/AP-E_M-Chapter-14-16-Part-3-Inductors/
excerpt: "A new device in the circuit - the inductor."
tags:
  - AP Physics C E&M
---

# 理想螺线管的 EMF

> 有一个长为 $l$、每单位长度有 $n$ 匝、半径为 $R$ 的理想螺线管。变化的电流 $I$ 通过螺线管，螺线管产生的 EMF 的大小为？

熟知理想螺线管内部

$$B = \mu_0 n I$$

每一匝的磁通量为 $B \times \pi R^2$，总共 $nl$ 匝：

$$\begin{aligned}
    \Phi_B &= nl \times B \times \pi R^2 \\
    &= \mu_0 \pi n^2 l R^2 I
\end{aligned}$$

$$\begin{aligned}
    \lvert \mathcal E \rvert &= \left\lvert \frac {d \Phi_B} {dt} \right\rvert \\
    &= \boxed{\mu_0 \pi n^2 l R^2 \left\lvert \frac {dI} {dt} \right\rvert}
\end{aligned}$$

# 电感

不难发现，对于很多产生 EMF 的电路元件，都有

$$\Phi_B \propto I \implies \mathcal E \propto \frac {dI} {dt}$$

不妨给这个比例系数起个名字，叫 inductance (电感)：

$$\boxed{
    L := \frac {\Phi_B} I
}$$

$$\Phi_B = LI \implies \mathcal E = - L \frac {dI} {dt}$$

电感的单位是 henry (H)。

回到前面的例子，不难发现理想螺线管的电感 $L = \mu_0 \pi n^2 l R^2$。

# 串并联等效

串联：

$$L = \sum L_i$$

并联：

$$\frac 1 L = \sum \frac 1 {L_i}$$

# 电感器的能量

$$\begin{aligned}
    U &= \int dW \\
    &= \int (\Delta V) dQ \\
    &= \int \left( L \frac {dI} {dt} \right) dQ \\
    &= \int LI dI \\
    &= \frac 1 2 L I^2 \\
\end{aligned}$$

# RL 电路

RL 电路串联了电源、电感器和电阻器。

## RL 电路充电

> 初始时电流为 $0$，求闭合开关后电路中的电流 $I(t)$。

$$\begin{cases}
    V + \mathcal E - IR = 0 \\
    \mathcal E = - L \frac {dI} {dt} \\
\end{cases} \implies V - L \frac {dI} {dt} - IR = 0$$

$$\begin{aligned}
    V - IR &= L \frac {dI} {dt} \\
    dt &= \frac {L dI} {V - IR} \\
    \frac R L dt &= \frac {dI} {\frac V R - I} \\
    \frac R L t &= - \ln \left( \frac V R - I \right) + C \\
    I &= \frac V R - C e^{- \frac R L t} \\
\end{aligned}$$

根据初值 $t = 0$ 时 $I = 0$，可得 $C = \frac V R$：

$$\boxed{
    I = \frac V R \left( 1 - e^{- \frac R L t} \right)
}$$

## RL 电路放电

> 初始时电流为 $I_0$，求接走电源（不难使用单刀双掷开关实现）后电路中的电流 $I(t)$。

$$\begin{aligned}
    - L \frac {dI} {dt} - IR &= 0 \\
    \frac {dI} {dt} &= - \frac R L I \\
\end{aligned}$$

熟知该微分方程的解：

$$\boxed{
    I = I_0 e^{- \frac R L t}
}$$

## Time constant

注意到关于 RL 电路的问题中都会遇到相同的指数项：

$$e^{- \frac R L t}$$

为了方便，定义指数 $-1$ 所需的时间，即指数项总体变为原来的 $\frac 1 e$ 所需的时间为 time constant $\tau$：

$$\boxed{
    \tau = \frac L R
}$$

# LC 电路

> LC 电路是串联了一个电容器和一个电感器的电路。
>
> 求电流 $I(t)$ 的通解。

$$\begin{cases}
    \frac 1 C Q - L \frac {dI} {dt} = 0 \\
    I = - \frac {dQ} {dt} \\
\end{cases} \implies \frac {d^2Q} {dt^2} + \frac 1 {LC} Q = 0$$

二阶常系数齐次 ODE，解得：

$$\boxed{
    Q = A \sin \left( \frac 1 {\sqrt{LC}} t + \varphi \right)
}$$

对 $t$ 求导得到电流：

$$I = - \frac {dQ} {dt} = - \frac A {\sqrt{LC}} \cos \left( \frac 1 {\sqrt{LC}} t + \varphi \right)$$

## 能量守恒

可以注意到总能量

$$\frac 1 2 \frac 1 C Q^2 + \frac 1 2 L I^2 = \frac {A^2} {2C}$$

是一个守恒量。