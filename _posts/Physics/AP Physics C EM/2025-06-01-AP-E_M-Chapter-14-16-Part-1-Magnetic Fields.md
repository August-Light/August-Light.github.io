---
title: 'AP E&M Chapter 14-16 Part 1: Magnetic Fields'
date: 2025-06-01
permalink: /posts/2025/06/AP-E_M-Chapter-14-16-Part-1-Magnetic Fields/
excerpt: "Biot-Savart Law, Lorentz Force, and Ampere's Law"
tags:
  - AP Physics C E&M
---

# Magnetic Field

The **magnetic field (磁场, 磁感应强度)** is a vector field, denoted by the symbol $\vec{B}$.

💡 $\vec{B}$ is a pseudovector.

A moving charge can produce a magnetic field, and it can also feel a force due to a magnetic field.

A current-carrying wire is an aggregate of moving charges. Therefore, it can produce and respond to a magnetic field as well.

|  | Produce $\vec{B}$ | Respond to $\vec{B}$ |
| :-: | :-: | :-: |
| Moving Charge | $\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{goldenrod}{q \vec{v}} \times \hat{r}} {r^2}$ | $\vec{F} = \textcolor{goldenrod}{q \vec{v}}  \times \vec{B}$ |
| Differential Length of Wire | $d\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{limegreen}{I d\vec{l}} \times \hat{r}} {r^2}$ | $d\vec{F} = \textcolor{limegreen}{I d\vec{l}} \times \vec{B}$ |

I'll elaborate on these 4 formulas.

## Magnetic Field due to a Point Charge

$$\boxed{
    \vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{goldenrod}{q \vec{v}} \times \hat{r}} {r^2}
}$$

$\vec{r}$ is defined as a position vector pointing from the location of the charge to the location where the magnetic field is calculated. $\hat{r}$ is the unit vector at this direction.

This is an experimental result.

$\mu_0$, **the permeability of free space (vacuum permeability, 真空磁导率)**, is a constant just like $\varepsilon_0$.

$$\mu_0 \approx 4\pi \times 10^{-7} \ \ce{T\cdot m/A}$$

where $\ce{T}$, **tesla**, is the unit for magnetic field.

## Magnetic Force on a Point Charge

The magnetic force on a point charge is given by

$$\boxed{
    \vec{F} = \textcolor{goldenrod}{q \vec{v}}  \times \vec{B}
}$$

From this formula, we can say $1 \ce{T} = 1 \ce{N\cdot s/(C\cdot m)} = 1 \ce{N/(A\cdot m)}$.

The direction of magnetic force is always perpendicular to that of the velocity, so it never does work on the point charge.

The **Lorentz force (洛伦兹力)** is the sum of the force due to the electric field and the force due to the magnetic field:

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \vec{F} = q (\vec{E} + \vec{v} \times \vec{B})
    }
$}$$

## Magnetic Field due to a Differential Length of Wire

Because of the principle of superposition, we only need to calculate $\sum q\vec{v}$ in the wire and then plug it into the yellow part of $\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{goldenrod}{q \vec{v}} \times \hat{r}} {r^2}$.

$$\begin{aligned}
    & \sum\limits_{i=1}^{dN} e\vec{v} \\
    =& e \vec{v}_D dN \\
    =& n e \vec{v}_D A dl \\
    =& I d\vec{l} & I = n e v_D A \\
\end{aligned}$$

$$\boxed{
    d\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{limegreen}{I d\vec{l}} \times \hat{r}} {r^2}
}$$

This formula is called the **Biot-Savart Law**. It's called a *law* because this formula was derived (by experiment and guess) earlier than $\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{goldenrod}{q \vec{v}} \times \hat{r}} {r^2}$.

## Magnetic Force on a Differential Length of Wire

Through the same process, we can derive

$$\boxed{
    d\vec{F} = \textcolor{limegreen}{I d\vec{l}} \times \vec{B}
}$$

# Gauss's Law for Magnetism

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \displaystyle \oint \vec{B} \cdot d\vec{A} = 0
    }
$}$$

This formula is similar to Gauss's Law for Electricity. However, because there are no **magnetic monopoles (磁单极子)**, $\rho_{\text{mag}} = 0$. Therefore, this law is also called **Absence of magnetic monopoles (无磁单极子定律)**.

## Example 14.1 Infinitely Long Wire

> What is the magnetic field at the point $(−r, 0)$ caused by an infinitely long wire carrying a current $I$ along the $y$-axis in the $+\hat{j}$-direction?

$$\begin{aligned}
    dB_z &= \frac {\mu_0} {4\pi} \frac {I dl} {(r^2 + y^2)} \sin \theta \\
    &= \frac {\mu_0} {4\pi} \frac {I dy} {(r^2 + y^2)} \frac r {\sqrt{r^2 + y^2}} \\
    &= \frac {\mu_0} {4\pi} \frac {Ir} {(r^2 + y^2)^{\frac 3 2}} dy \\
\end{aligned}$$

$$\begin{aligned}
    B &= \int dBa \\
    &= \frac {\mu_0 I r} {4\pi} \int_{-\infty}^{+\infty} \frac 1 {(r^2 + y^2)^{\frac 3 2}} dy \\
    &= \frac {\mu_0 I r} {4\pi} \int_{-\frac \pi 2}^{\frac \pi 2} \frac 1 {(r^2 + r^2 \tan^2 \theta)^{\frac 3 2}} (r \sec^2 \theta d\theta) & y = r \tan \theta \\
    &= \frac {\mu_0 I} {4\pi r} \int_{-\frac \pi 2}^{\frac \pi 2} \cos\theta d\theta \\
    &= \frac {\mu_0 I} {2\pi r} \\
\end{aligned}$$

$$\boxed{\vec{B} = \frac {\mu_0 I} {2\pi r} \hat{k}}$$

## Example 14.2 The Force Between Parallel Wires

> Given two infinitely long parallel wires lying on the $xy$-plane, what is the force per length exerted on wire 1 by wire 2?

$$\begin{aligned}
    \frac {F_{\text{on 1}}} l &= I_1 B \\
    &= \frac {\mu_0 I_1 I_2} {2\pi r}
\end{aligned}$$

# Ampere’s law

Ampere’s law is a restatement of the Biot-Savart law.

$$\boxed{
    \oint \vec{B} \cdot d\vec{l} = \mu_0 I_{\text{enclosed}}
}$$

It's a line integral. The positive direction of $I_{\text{enc}}$ is determined by the right-hand rule.

Ampere's Law is not complete - it is only valid when an electric field is static. We will soon generalize it to Ampere-Maxwell law to deal with situations where this is not the case.

I'm not gonna prove it because it's as complicated as Gauss's Law for Electricity 😒.

## Example 14.4

> Solve Example 14.1 with Ampere's law.

Use a circular Amperian path that lies in a plane perpendicular to the wire.

$$\begin{aligned}
    \oint \vec{B} \cdot d\vec{l} &= \mu_0 I_{\text{enc}} \\
    (2\pi r) B &= \mu_0 I \\
    B &= \frac {\mu_0 I} {2\pi r} \\
\end{aligned}$$