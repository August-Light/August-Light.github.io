---
title: 'AP E&M Chapter 14-16 Part 2: Faraday’s Law'
date: 2025-06-01
permalink: /posts/2025/06/AP-E_M-Chapter-14-16-Part-2-Faradays-Law/
excerpt: "Magnetic fields can produce electric fields."
tags:
  - AP Physics C E&M
---

# 感应电动势

电荷受到 Lorentz 力而额外产生的电压被称为**感应电动势 (induced EMF)**：

$$\boxed{
    \mathcal E := \oint \frac {\bm F} q \cdot d \bm l = \oint (\bm E + \bm v \times \bm B) \cdot d \bm l
}$$

把这个式子拆成两项：

$$\mathcal E = \boxed{\oint \bm E \cdot d \bm l} + \boxed{\oint (\bm v \times \bm B) \cdot d \bm l}$$

前一项被称为感生电动势，后一项被称为动生电动势。

## 关于 $\bm v$

此处的 $\bm v$ 是指电荷运动速度，但是「导线中的电荷运动速度」往往是不太好用的。

我们做一个分解：

$$\bm v_{\text{charge}} = \bm v_{\text{wire}} + \bm u$$

其中 $\bm u$ 表示电荷**相对导线**的运动速度。由于 $\bm u \parallel d \bm l$：

$$(\bm u \times \bm B) \cdot d \bm l = 0$$

因此

$$\begin{aligned}
    & \oint (\bm E + \bm v_{\text{charge}} \times \bm B) \cdot d \bm l \\
    =& \oint (\bm E + (\bm v_{\text{wire}} + \bm u) \times \bm B) \cdot d \bm l \\
    =& \oint (\bm E + \bm v_{\text{wire}} \times \bm B) \cdot d \bm l \\
\end{aligned}$$

因此我们发现把 $\bm v$ 解释为导线运动速度也是正确的！这下就好用多了。

# Faraday 电磁感应定律

定义**磁通量**：

$$\boxed{
    \Phi_B := \iint \bm B \cdot d \bm A
}$$

对于**不论在不在运动 / 形变**的回路，以及**不论在不在变化**的磁场，以下**实验定律**均成立，称为 **Faraday 电磁感应定律 (Faraday’s Law)**：

$$\boxed{
    \mathcal E = - \frac {d \Phi_B} {dt}
}$$

## 感生电动势

对于静止回路，有 $\bm v = 0$，因此只有感生电动势：

$$\boxed{
    \oint \bm E \cdot d \bm l = - \frac {d \Phi_B} {dt}
}$$

当然，在回路不动的情况下，对时间求全导数相当于对磁场求偏导数。等式右侧也可以写成：

$$\oint \bm E \cdot d \bm l = - \iint \frac{\partial \bm B} {\partial t} \cdot d \bm A$$

怎么解读这个式子呢？可以认为，是**磁场的变化导致了涡旋电场的产生**：

$$\frac {\partial \bm B} {\partial t} \implies \nabla \times \bm E$$

取一个极限：

$$\boxed{
    \nabla \times \bm E = - \frac {\partial \bm B} {\partial t}
}$$

## 用磁场表示

💡 根据 Reynolds transport theorem / Leibniz integral rule，我们也可以把感应电动势完全用磁场写出来：

$$\mathcal E = - \iint \frac {\partial \bm B} {\partial t} \cdot d \bm A + \oint (\bm v \times \bm B) \cdot d \bm l$$

# 例题

## Example 18.2

> Consider a flat loop of wire area $A$ rotating at a constant angular velocity $\omega$ within a constant magnetic field of magnitude $B$. What are the maximum and minimum magnitudes of the induced EMF in the loop?

$$\begin{aligned}
    \lvert \mathcal E \rvert &= \left\lvert \frac {d \Phi_B} {dt} \right\rvert \\
    &= \left\lvert \frac d {dt} (\bm B \cdot \bm A) \right\rvert \\
    &= \left\lvert \frac d {dt} (AB \cos \theta) \right\rvert \\
    &= \lvert \omega A B \sin \theta \rvert
\end{aligned}$$

最小值为 $0$，最大值为 $\omega A B$。

## Example 18.4

> The current passing through an infinitely long solenoid of radius $R$ with $n$ turns per length is given as a function of time, $I(t)$. What is the magnitude of the electric field a distance $a > R$ from the center of the solenoid?

通过 Ampere 环路定律可以证明熟知结论：理想无限长通电螺线管中，内部 $B = \mu_0 n I$，外部 $B = 0$。

取一个半径为 $a$ 的圆作为回路：

$$\begin{aligned}
    \oint \bm E \cdot d \bm l &= \left\lvert \frac {d \Phi_B} {dt} \right\rvert \\
    2 \pi E a &= \left\lvert \mu_0 n \frac {dI} {dt} \times \pi R^2 \right\rvert \\
    E &= \frac {\mu_0 R^2 n} {2a} \left\lvert \frac {dI} {dt} \right\rvert \\
\end{aligned}$$

## Example 18.6

> Consider Figure 18.8. Both situations feature a bar of length $\lambda$, moving to the right with speed $v$ in a uniform magnetic field B going into the page. The only difference is that in Figure 18.8(A) the bar is connected to a circuit, whereas in Figure 18.8(B) it is not part of a closed circuit.
>
> <img src="https://cdn.luogu.com.cn/upload/image_hosting/dfgqmip3.png" width=400/>
>
> (a) Calculate the EMF induced in the loop to the left of the bar in Figure 18.8(A). In what direction does the current flow?
>
> (b) Positive charges within the bar feel a magnetic force toward the top of the page, due to their motion to the right. Therefore, in Figure 18.8(B) positive charge accumulates at the top of the rod, producing a downward electric field. After the rod has been moving with constant velocity for a long time, the charge reaches equilibrium so that the downward electric force on charges in the rod exactly cancels the upward magnetic force and charges do not move up or down the rod. What are the magnitude and direction of this electric field?

### (a)

$$\begin{aligned}
    \mathcal E &= - \frac {d \Phi_B} {dt} \\
    &= - \frac {- B l dx} {dt} \\
    &= B l v \\
\end{aligned}$$

### (b)

Equilibrium 时，每个电荷都受力平衡：

$$\begin{aligned}
    q (\bm E + \bm v \times \bm B) &= 0 \\
    \bm E &= - \bm v \times \bm B \\
    E &= vB \\
\end{aligned}$$

事实上，导体棒开始运动的一瞬间，equilibrium 就被建立。