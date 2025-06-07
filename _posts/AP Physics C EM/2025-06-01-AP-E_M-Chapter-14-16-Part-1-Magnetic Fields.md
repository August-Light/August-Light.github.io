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
| Moving Charge | $\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{yellow}{q \vec{v}} \times \hat{r}} {r^2}$ | $\vec{F} = \textcolor{yellow}{q \vec{v}}  \times \vec{B}$ |
| Differential Length of Wire | $d\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{lightgreen}{I d\vec{l}} \times \hat{r}} {r^2}$ | $d\vec{F} = \textcolor{lightgreen}{I d\vec{l}} \times \vec{B}$ |

I'll elaborate on these 4 formulas.

## Magnetic Field due to a Point Charge

$$\boxed{
    \vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{yellow}{q \vec{v}} \times \hat{r}} {r^2}
}$$

$\vec{r}$ is defined as a position vector pointing from the location of the charge to the location where the magnetic field is calculated. $\hat{r}$ is the unit vector at this direction.

This is an experimental result.

$\mu_0$, **the permeability of free space (vacuum permeability, 真空磁导率)**, is a constant just like $\varepsilon_0$.

$$\mu_0 \approx 4\pi \times 10^{-7} \ \ce{T\cdot m/A}$$

where $\ce{T}$, **tesla**, is the unit for magnetic field.

## Magnetic Force on a Point Charge

The magnetic force on a point charge is given by

$$\boxed{
    \vec{F} = \textcolor{yellow}{q \vec{v}}  \times \vec{B}
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

Because of the principle of superposition, we only need to calculate $\sum q\vec{v}$ in the wire and then plug it into the yellow part of $\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{yellow}{q \vec{v}} \times \hat{r}} {r^2}$.

$$\begin{aligned}
    & \sum\limits_{i=1}^{dN} e\vec{v} \\
    =& e \vec{v}_D dN \\
    =& n e \vec{v}_D A dl \\
    =& I d\vec{l} & I = n e v_D A \\
\end{aligned}$$

$$\boxed{
    d\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{lightgreen}{I d\vec{l}} \times \hat{r}} {r^2}
}$$

This formula is called the **Biot-Savart Law**. It's called a *law* because this formula was derived (by experiment and guess) earlier than $\vec{B} = \frac {\mu_0} {4\pi} \frac {\textcolor{yellow}{q \vec{v}} \times \hat{r}} {r^2}$.

## Magnetic Force on a Differential Length of Wire

Through the same process, we can derive

$$\boxed{
    d\vec{F} = \textcolor{lightgreen}{I d\vec{l}} \times \vec{B}
}$$

# Gauss's Law for Magnetism

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \displaystyle \oint \vec{B} \cdot d\vec{A} = 0
    }
$}$$

This formula is similar to Gauss's Law for Electricity. However, because there are no **magnetic monopoles (磁单极子)**, $\rho_{\text{mag}} = 0$. Therefore, this law is also called **Absence of magnetic monopoles (无磁单极子定律)**.

# Ampere’s law

Ampere’s law is a restatement of the Biot-Savart law.

$$\boxed{
    \oint \vec{B} \cdot d\vec{l} = \mu_0 I_{\text{enclosed}}
}$$

I'm not gonna prove it because it's as complicated as Gauss's Law for Electricity 😒.

## Example 1

TODO:

