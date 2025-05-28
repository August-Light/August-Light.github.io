---
title: 'AP Physics C Mechanics Chapter 9 Simple Harmonic Motion'
date: 2025-03-23
permalink: /posts/2025/03/AP-Physics-C-Mechanics-Chapter-9-Simple-Harmonic-Motion/
excerpt: "Intro to simple harmonic motion."
tags:
  - AP Physics C Mech
---

# Vocabulary
- Simple pendulum 单摆
- Amplitude 振幅 $A$
- Angular frequency 圆频率 $\omega$
- (Linear) frequency 频率 $f$
- Period 周期 $T$
- Phase 相位 $\omega x + \varphi$
- Initial phase 初始相位 $\varphi$

# Math Time

The solution to the second-order differential equation

$$\frac {d^2 x} {dt^2} + b x = 0$$

is

$$x(t) = C_1 \sin(\sqrt b x) + C_2 \cos(\sqrt b x)$$

which is equivalent to (for non trivial solutions)

$$\boxed{x(t) = A \sin(\sqrt b x + \varphi)}$$

# SHM

<https://en.wikipedia.org/wiki/Simple_harmonic_motion>

Simple harmonic motion (SHM) is a special type of periodic motion an object experiences by means of a restoring force whose magnitude is directly proportional to the distance of the object from an equilibrium position and acts towards the equilibrium position.

# Angular Frequency, Linear Frequency, and Period

The angular frequency of $A \sin (\omega x + \varphi)$ is $\omega$.

The linear frequency is defined as:

$$\boxed{f = \frac {\omega} {2 \pi}}$$

The period, defined as the time per cycle, is the inverse of the frequency:

$$\boxed{T = \frac 1 f}$$

$$\boxed{f = \frac {\omega} {2\pi} = \frac 1 T}$$

# Example 9.1 Simple Pendulum

> Calculate the frequency of oscillation of a simple pendulum of length $L$, assuming small oscillations.

(See Figure 9.4)

$$\begin{aligned}
    \tau = I \alpha &= - mgl \sin \theta \\
    I \alpha &\approx -mgl \theta & \text{for small oscillations} \\
    \frac {d^2 \theta} {dt^2} + \frac {mgl} I \theta &= 0 \\
\end{aligned}$$

Solving this second-order differential equation, we get:

$$\theta = A \sin\left( \sqrt{\frac {mgl} I} t + \varphi \right)$$

Which means that the angular frequency is:

$$\omega = \sqrt {\frac {mgl} I} = \sqrt {\frac {mgl} {ml^2}} = \sqrt {\frac g l}$$

And we can now calculate the linear frequency as well:

$$f = \frac \omega {2 \pi} = \frac 1 {2\pi} \sqrt {\frac g l}$$

---

From this example, we derived **the angular frequency for a simple pendulum (assuming small oscillations)**:

$$\boxed{\omega = \sqrt {\frac g l}}$$

# The $k_{\text{effective}}$ method

We use the slope of $F(x)$ or $\tau(\theta)$ at $x = 0$ or $\theta = 0$ to approximate $F(x)$ or $\tau(\theta)$:

$$\boxed{k_{\text{effective}} = \left.-\frac {dF} {dx} \right|_{\text{equilibrium distance}}}$$

$$\boxed{k_{\text{effective}} = \left.-\frac {d\tau} {d\theta} \right|_{\text{equilibrium distance}}}$$

Then we can calculate the angular frequency for a SHM system:

$$\boxed{\omega = \sqrt {\frac {k_{\text{effective}}} m}}$$

$$\boxed{\omega = \sqrt {\frac {k_{\text{effective}}} I}}$$

# Example 9.2 Mass-Spring System

> What is the general mathematical description of a mass connected to a spring oscillating on a horizontal frictionless surface?

$$\begin{aligned}
    F = ma &= -kx \\
    \frac {d^2 x} {dt^2} + \frac k m x &= 0 \\
\end{aligned}$$

Solving this second-order differential equation, we get:

$$x(t) = A \sin\left( \sqrt {\frac k m} t + \varphi \right)$$

# Example 9.3 A Vertical Spring System

> A mass hanging from a spring (spring constant $k$) is at rest.
>
> (a) What is the equilibrium extension of the spring?
>
> (b) What is the angular frequency of oscillation about this equilibrium point?

$$\begin{aligned}
    F &= -kx + mg \\
    a &= - \frac k m x + g \\
    \frac {d^2 x} {dt^2} + \frac k m x &= g \\
    x &= A \sin(\sqrt{\frac k m} t + \varphi) + \frac {mg} k \\
\end{aligned}$$

The extension of the spring is given by $\frac {mg} k$, and the angular frequency is $\sqrt {\frac k m}$.

# Example 9.4

> A $2$ kg mass is oscillating on a spring with a spring constant of $10$ N/m. When the spring is stretched $1$ m, the velocity of the mass is $13$ m/s. What is the amplitude of the oscillation?

## Solution 1 (from the book)

Energy conservation (when the spring is maximally stretched, it has zero speed):

$$\begin{aligned}
    \frac 1 2 m v^2 + \frac 1 2 k x^2 &= \frac 1 2 k x_{\max}^2 \\
    \frac 1 2 (2kg) (13m/s)^2 + \frac 1 2 (10N/m) (1m)^2 &= \frac 1 2 (10N/m) x_{\max}^2 \\
    x_{\max} &= \sqrt{\frac {174} 5}m \approx \boxed{5.899m} \\
\end{aligned}$$

## Solution 2

We know

$$x(t) = A \sin\left( \sqrt {\frac k m} t + \varphi \right)$$

Differentiate both sides:

$$v(t) = A \cos\left( \sqrt {\frac k m} t + \varphi \right) \times \sqrt {\frac k m}$$

Plug the given data into these formulas:

$$\begin{cases}
    x(0) = A \sin \varphi = 1m \\
    v(0) = A \cos \varphi \times \sqrt 5 s^{-1} = 13m/s \\
\end{cases}$$

$$A = \sqrt {\frac {174} 5}m  \approx \boxed{5.899m}$$

# Example 9.5 Physical Pendulum

> (See page 256)

## (a)

From Example 9.1, we know $\omega = \sqrt {\frac {mgl} I}$:

$$\omega = \sqrt {\frac {mgl} I} = \sqrt{40} s^{-1} \approx \boxed{6.325} s^{-1}$$

## (b)

$$U = mgh = mgd(1 - \cos \theta) = (20J) (1 - \cos\theta)$$

## (c) Solution 1 (from the book)

Energy conservation:

$$E_{\text{mech}} = U + KE = mgd(1 - \cos\theta) + \frac 1 2 I \omega^2$$

$$(20J)(1 - \cos 0.1) + \frac 1 2 (0.5 kg \cdot m^2) (0.05 s^{-1})^2 = 0 + \frac 1 2 (0.5 kg \cdot m^2) \omega_{\max}^2$$

$$\omega_{\max} = \frac {\sqrt {161}} {20} s^{-1} \approx \boxed{0.634 s^{-1}}$$

## (c) Solution 2

Follow the same way in Solution 2 of Example 9.4:

$$\begin{cases}
    \theta(1s) = A \sin \left( \sqrt{40} + \varphi \right) = 0.1 \\
    \tau(1s) = A \cos \left( \sqrt{40} + \varphi \right) \times \sqrt{40} s^{-1} = 0.05 s^{-1} \\
\end{cases}$$

$$A = \frac {\sqrt{1610}} {400}$$

$$\omega_{\max} = A \times \sqrt{40} s^{-1} = \frac {\sqrt {161}} {20} s^{-1} \approx \boxed{0.634 s^{-1}}$$