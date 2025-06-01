---
title: 'AP E&M Chapter 13.5 Other things about Circuits'
date: 2025-05-19
permalink: /posts/2025/05/AP-E_M-Chapter-13_5-Other-things-about-Circuits/
excerpt: 'Concepts about circuits.'
tags:
  - AP Physics C E&M
---

# Current Density and Drift Velocity

## Current Density

The **current density (电流密度)** $\vec{J}$ is a vector field within a wire.

$$\boxed{
    I = \int \vec{J} \cdot d\vec{A}
}$$

Suppose a uniform current flows through a straight wire, $\vec{J}$ is constant and parallel to $d\vec{A}$. Therefore, **the current density for the case of a straight wire** is

$$\boxed{
    J = \frac I A
}$$

## Drift Velocity

The **drift velocity (漂移速度)** is defined as the average electron velocity:

$$\boxed{
    \vec{v}_D = \frac 1 N \sum\limits_{i=1}^N \vec{v}_i
}$$

## Relationship between Current Density & Drift Velocity

The **charge carrier density $n$ (载流子密度)** denotes the number of charge carriers per volume. The SI unit for charge carrier density is $\ce{m^{-3}}$.

$$\begin{aligned}
    J &= \frac I A \\
    &= \frac 1 A \frac {dQ} {dt} \\
    &= \frac 1 A \frac {e dN} {dt} \\
    &= \frac 1 A \frac {n e A v_D dt} {dt} \\
    &= n e v_D
\end{aligned}$$

Therefore, the relationship between current density and drift velocity is

$$\boxed{
    \vec{J} = n e \vec{v}_D
}$$

$e$ is the **elementary charge (元电荷)**, which is electric charge carried by a single proton.

$$e = 1.602176634 \times 10^{-19} \ \ce{C}$$

# Resistivity & Conductivity

**Resistivity (电阻率)** is defined as the ratio of the electric field to the current density:

$$\boxed{
    \vec{E} = \rho \vec{J}
}$$

$$\boxed{
    \rho = \frac E J
}$$

This is known as a [reformulation of Ohm's law](https://en.wikipedia.org/wiki/Ohm%27s_law).

**Conductivity (电导率)** is defined as the reciprocal of resistivity.

$$\boxed{
    \sigma = \frac 1 \rho = \frac J E
}$$

>  Resistivity and conductivity are **properties of materials**. Resistance depends on the material and the geometry of the object.

---

$$\begin{aligned}
    R &= \frac V I \\
    &= V \frac 1 {JA} \\
    &= V \frac \rho {EA} \\
    &= V \frac \rho {\frac V L A} \\
    &= \frac {\rho L} A
\end{aligned}$$

Therefore, **the resistance of a resistor with length $L$, cross-sectional area $A$, and resistivity $\rho$** is

$$\boxed{
    R = \frac {\rho L} A
}$$