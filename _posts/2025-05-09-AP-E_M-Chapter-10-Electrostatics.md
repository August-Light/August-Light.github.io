---
title: 'AP E&M Chapter 10 Electrostatics'
date: 2025-05-09
permalink: /posts/2025/05/AP-E_M-Chapter-10-Electrostatics/
excerpt: 'Intro to E&M - Electrostatics.'
tags:
  - AP Physics C E&M
---

<!--Used $\ce{}$ to write units in formulas-->

# Coulomb's Law

The magnitude of the **electrostatic force** (静电力) between to point charges (点电荷) $Q_1$ and $Q_2$ separated by a distance $R$ is given by the equation

$$\boxed{
    F = \frac {\lvert Q_1 \rvert \lvert Q_2 \rvert} {4 \pi \varepsilon_0 R^2}
}$$

The direction of the force is along the line between the two charges. **Like charges repel**, while **unlike charges attract**.

The constant $\varepsilon_0$ is called **the permittivity of free space** (真空介电常数 / 电常数), which is the constant ratio of $\frac {\lvert Q_1 \rvert \lvert Q_2 \rvert} {4 \pi R^2}$ to $F$.

$$\varepsilon_0 \approx 8.85 \times 10^{-12} \ \ce{C^2/N\cdot m}$$

$4 \pi R^2$ in the denominator is the surface area of a sphere of radius $R$, which is consistent with the propagation of electrostatic force in 3D space.

---
An alternative form for this formula is:

$$\boxed{
    F = k \frac {\lvert Q_1 \rvert \lvert Q_2 \rvert} {R^2}
}$$

where $k = \frac 1 {4 \pi \varepsilon_0} \approx 8.99 \times 10^9 \ \ce{N\cdot m^2/C^2}$ is called the **electrostatic constant** (静电力常量), as an analog of $G$ in Newton's law of universal gravitation.

# Electric Field

Like a gravitational field ($\vec{g} = \frac {\vec{F}} m$), we can define

$$\boxed{
    \vec{E} = \frac {\vec{F}_{\text{test}}} {Q_{\text{test}}}
}$$

where $\vec{E}$ is called the **electric field** (电场).

By Coulomb's Law, we can derive that the magnitude of an electric field due to a point charge $Q$ is

$$\boxed{
    E = \frac {\lvert Q \rvert} {4 \pi \varepsilon_0 R^2}
}$$

(direction is away from positive point charges and toward negative point charges)

## The Principle of Superposition

$$\vec{E}_{\text{net}} = \frac {\vec{F}_{\text{net}}} Q = \sum \frac {\vec{F}} {Q} = \sum \vec{E}$$

Therefore,

$$\boxed{
    \vec{E}_\text{net} = \sum \vec{E}
}$$

## Visualizing: Electric Field Lines

> An electric field line is an imaginary line or curve drawn through a region of empty space so that **its tangent at any point is in the direction of the electric field vector at that point**. ([Electric Field Lines - Brilliant Math & Science Wiki](https://brilliant.org/wiki/electric-field-lines/))

- The lines represent the direction of the force.
- The lines always begin on a positive charge and end on a negative charge.
- The lines may never intersect in a location where the direction of the electric field is well defined.

![Image from Wiki](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Camposcargas.svg/500px-Camposcargas.svg.png)

## Electrostatic Induction (静电感应)

When a point charge $+Q$ is placed near an uncharged metal, the negative charge in the metal is attracted while the positive charge in the metal is repelled. Because negative charge is closer, the attraction force is greater than the repulsion force, creating a net attractive force.

# Electric potential & Voltage

The **electric potential** $V$ (电势) is an electrical analog of the $gh$ part in $U = mgh$, which is the formula for gravitational potential energy. It reveals properties of the **field** and is independent of the object.

$$\boxed{
    V = \frac U q \iff \Delta V = \frac {\Delta U} q \iff dV = \frac {dU} q
}$$

$$\begin{aligned}
    V(r) &= \int_{x=\infty}^{x=r} dV \\
    &= \int \frac 1 q dU \\
    &= \int_\infty^r \frac F q dx \\
    &= \frac Q {4 \pi \varepsilon_0 r}
\end{aligned}$$

$$\boxed{
    V(r) = \int_{x=\infty}^{x=r} dV = \frac Q {4 \pi \varepsilon_0 r}
}$$

The difference in potential energy is called **voltage** (电压).

The units of electric potential and voltage are **volts**, given by $1 \ \text{volt} = 1 \ \ce{V} = 1 \ \ce{J/C}$.

> One **electronvolt** (电子伏特) is the amount of energy stored by a charge of $e$ when it moves through a potential difference of $1$ volt: $1 \ \text{eV} = 1.602176634 \times 10^{-19} \ \text{J} \approx 1.60 \times 10^{-19} \ \text{J}$. It is a measure of **energy** instead of voltage.

## The Principle of Superposition

$$\boxed{
    V_{\text{net}} = \sum V
}$$

## Relationship Between Potential and Electric Field

Starting with the relationship between potential energy and force,

$$\vec{F} = - \nabla U$$

(For 1D situation: $F = - \frac {dU} {dx}$)

Dividing both sides by the charge yields

$$\boxed{
    \vec{E} = - \nabla V
}$$

(For 1D situation: $\boxed{E = - \frac {dV} {dx}}$)

---

Integrate backwards we can derive

$$\boxed{
    \Delta V = - \int \vec{E} \cdot d\vec{s}
}$$

(For 1D situation: $\boxed{\Delta V = - \int E \cdot dx}$)

## Visualizing: Equipotential Lines (等势线)

> Equipotential lines are lines of constant potential in the 2D plane.

- No work is required to move a charge along an equipotential line.
- Equipotential lines are always **perpendicular** to electric field lines.
- $\vec{E}$ is stronger where equipotential lines are spaced closely together. (Because $\vec{E} = \nabla V$)

# Calculation

## Example 10.3 & 10.9

> A rod containing a uniformly distributed charge $+Q$ extends along the $x$-axis from $x = a$ to $x = b$. Calculate the potential and the electric field at the origin.

$\lambda = \frac Q {b-a}$

$$\begin{aligned}
    V &= \int dV \\
    &= \int \frac {dQ} {4 \pi \varepsilon_0 r} \\
    &= \int_a^b \frac {\lambda dr} {4 \pi \varepsilon_0 r} \\
    &= \frac {\lambda} {4 \pi \varepsilon_0} \ln\left( \frac b a \right) \\
    &= \frac Q {4 \pi \varepsilon_0 (b-a)} \ln\left( \frac b a \right) \\
\end{aligned}$$

---

$$\begin{aligned}
    E &= \int dE \\
    &= \int \frac {dQ} {4\pi\varepsilon_0 r^2} \\
    &= \int_a^b \frac {\lambda dr} {4\pi\varepsilon_0 r^2} \\
    &= \frac \lambda {4\pi\varepsilon_0} \left( \frac 1 a - \frac 1 b \right) \\
    &= \frac Q {4\pi\varepsilon_0 (b-a)} \left( \frac 1 a - \frac 1 b \right) \\
\end{aligned}$$

$$\vec{E} = \frac Q {4\pi\varepsilon_0 (b-a)} \left( \frac 1 a - \frac 1 b \right) \hat i$$

## Example 10.4

> Consider a spherical charge distribution of inner radius $a$ and outer radius $b$. The volume charge distribution is given by the formula $\rho(r) = kr$, where $k$ is a proportionality constant with units $\ce{C\cdot m^{−4}}$. Compute the potential at the center of the spherical shell.

$$\begin{aligned}
    V &= \int dV \\
    &= \int \frac {dQ} {4 \pi \varepsilon_0 r} \\
    &= \int_a^b \frac {\rho(r) \times 4 \pi r^2 dr} {4 \pi \varepsilon_0 r} \\
    &= \frac k {3 \varepsilon_0} (b^3 - a^3) \\
\end{aligned}$$

This example clearly shows why we add a $4\pi$ in the Coulomb's Law formula.

## Example 10.11

> A charge $+Q$ is evenly distributed in a ring of radius $a$ on the $xy$-plane centered at the origin. What is the magnitude of the electric field at a point along the $z$-axis $(0, 0, b)$?

Dur to symmetry, we can just calculate the electric field on the $z$-direction:

$$\begin{aligned}
    E &= \frac b {\sqrt{a^2 + b^2}} \times \frac Q {4\pi\varepsilon_0 (a^2 + b^2)} \\
    &= \frac {Qb} {4\pi\varepsilon_0 (a^2+b^2)^{\frac 3 2}} \\
\end{aligned}$$

## Example 10.6 & 10.12

> Consider a charge $+Q$ distributed evenly along a flat circular surface of radius $a$. What is the potential and the electric field a distance $d$ from the surface along the perpendicular running through the center of the circle?

$\sigma = \frac Q {\pi a^2}$

$$\begin{aligned}
    V &= \int dV \\
    &= \int \frac {dQ} {4 \pi \varepsilon_0 \sqrt{r^2 + d^2}} \\
    &= \int_0^a \frac {\sigma \times 2 \pi r dr} {4\pi\varepsilon_0 \sqrt{r^2 + d^2}} \\
    &= \frac \sigma {2\varepsilon_0} (\sqrt{a^2 + d^2} - d) \\
    &= \frac Q {2 \pi \varepsilon_0 a^2} (\sqrt{a^2 + d^2} - d) \\
\end{aligned}$$

---

$$\begin{aligned}
    E &= \int dE \\
    &= \int \frac {dQ \times d} {4\pi\varepsilon_0 (r^2 + d^2)^{\frac 3 2}} & \text{Example 10.11} \\
    &= \int \frac {\sigma \times 2\pi r dr} {4\pi\varepsilon_0 (r^2 + d^2)^{\frac 3 2}} \\
    &= \frac {\sigma d} {2 \varepsilon_0} \int_0^a \frac r {(r^2 + d^2)^{\frac 3 2}} dr \\
    &= \frac {\sigma d} {2 \varepsilon_0} \left( \frac 1 d - \frac 1 {\sqrt{a^2 + d^2}} \right) \\
    &= \frac {Qd} {2\pi\varepsilon_0 a^2} \left( \frac 1 d - \frac 1 {\sqrt{a^2 + d^2}} \right) \\
\end{aligned}$$