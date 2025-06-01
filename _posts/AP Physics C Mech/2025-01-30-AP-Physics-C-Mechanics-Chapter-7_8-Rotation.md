---
title: 'AP Physics C Mechanics Chapter 7&8 Rotation'
date: 2025-01-30
permalink: /posts/2025/01/AP-Physics-C-Mechanics-Chapter-7_8-Rotation/
excerpt: "Intro to concepts in rotation."
tags:
  - AP Physics C Mech
---

# Vocabulary

- Rigid body 刚体
- Angular position 角位置 $\theta$
- Angular displacement 角位移 $\Delta \theta$
- Angular velocity 角速度 $\omega$
- Angular acceleration 角加速度 $\alpha$
- Rotational kinetic energy 旋转动能 $KE_{\text{rotational}}$
- Rotational inertia 转动惯量 $I$
- Torque 扭矩 $\tau$
- Angular momentum 角动量 $L$

# Angular Quantities

Angular displacement:

$$\boxed{\Delta \theta = \theta_{\text{final}} - \theta_{\text{initial}}}$$

Angular velocity:

$$\boxed{\omega = \frac {d \theta} {dt}}$$

Angular acceleration:

$$\boxed{\alpha = \frac {d \omega} {dt} = \frac {d^2 \theta} {dt^2}}$$

## Equations

Valid only for **uniformly accelerated motion (UAM)**:

$$\omega = \omega_0 + \alpha t$$

$$\omega^2 = \omega_0^2 + 2 \alpha \Delta \theta$$

# Relationships Between Angular and Linear Quantities

Differentiate both sides of $s = r \theta$ with respect to $t$:

$$\boxed{v = \omega r}$$

Differentiate both sides again:

$$\boxed{a_{\text{tan}} = \alpha r}$$

---

In Chapter 3 we derived:

$$\boxed{a_{\text{radial}} = \omega v = \frac {v^2} r = \omega^2 r}$$

## 💡 Pseudo-vectors (Axial vectors)

The direction of $\vec{\omega}$ is normal to the plane of rotation (or the angular displacement $\Delta \theta$).

To ensure the relationship $v = \omega r$ holds, we define:

$$\boxed{\vec{v} = \vec{\omega} \times \vec{r}}$$

Taking the derivative with respect to $t$ on both sides of the equation, we derived:

$$\vec{a} = \frac {d \vec{\omega}} {dt} \times \vec{r} + \vec{\omega} \times \frac {d \vec{r}} {dt}$$

$$\boxed{\vec{a}_{\tan} = \vec{\alpha} \times \vec{r}} \text{ and } \boxed{\vec{a}_{\text{radial}} = \vec{\omega} \times \vec{v}}$$

$$\boxed{\vec{a} = \vec{a}_{\tan} + \vec{a}_{\text{radial}} = \vec{\alpha} \times \vec{r} + \vec{\omega} \times \vec{v}}$$

Angular quantities are pseudo-vectors, which means they act like vectors in normal circumstances but act differently when the world is reflected.

- <https://physics.stackexchange.com/questions/455119/centripetal-acceleration-as-a-cross-product>
- <https://www.zhihu.com/question/52389348>

# Translational KE $\to$ Rotational KE

Divide the object into infinitely small pieces and sum the KE of each piece:

$$\begin{aligned}
    KE_{\text{rotational}} &= \int \frac 1 2 v^2 dm \\
    &= \frac 1 2 \int r^2 \omega^2 dm \\
    &= \frac 1 2 \omega^2 \int r^2 dm \\
\end{aligned}$$

This equation is very similar to $KE = \frac 1 2 m v^2$, which is the equation for translational KE. $\int r^2 dm$ is the angular analog of mass.

Just as mass is a measure of translational inertia, this integral is a measure of rotational inertia:

$$\boxed{I = \int r^2 dm}$$

(Which is the definition of rotational inertia)

We can rewrite the equation for rotational kinetic energy:

$$\boxed{KE_{\text{rotational}} = \frac 1 2 I \omega^2}$$

# Mass $\to$ Rotational inertia

## Example 8.1

> A rod of uniform density and total mass $m$ extends from the origin to the point $(L,0,0)$. Calculate its rotational inertia if rotated about the $z$-axis.

$$\begin{aligned}
    I &= \int r^2 dm \\
    &= \int_0^L r^2 \times \lambda \times dx \\
    &= \frac 1 3 \lambda L^3 \\
    &= \boxed{\frac 1 3 m L^2} \\
\end{aligned}$$

($\lambda$ is the linear density; similarly, area density is represented by $\sigma$)

## Example 8.3

> A planar circular mass distribution of radius $R$ centered at the origin (and lying in the $xy$-plane) is rotating about the $x$-axis. The object's mass $M$ is distributed uniformly. Calculate the rotational inertia.

We have $dA = 2 \sqrt{R^2 - y^2} dy$ and $\sigma = \frac {M} {\pi R^2}$. Therefore, we can calculate $dm$:

$$dm = \sigma dA = \frac {2M} {\pi R^2} \sqrt{R^2 - y^2} dy$$

$$\begin{aligned}
    I =& \int r^2 dm \\
    =& \int_{-R}^R y^2 \frac {2M} {\pi R^2} \sqrt{R^2 - y^2} dy \\
    =& \frac {2M} {\pi R^2} \int_{-R}^R y^2 \sqrt{R^2 - y^2} dy \\
\end{aligned}$$

This integral is a little bit tricky. We can solve it by using a trigonometric substitution:

$$\begin{aligned}
    & \int_{-R}^R y^2 \sqrt{R^2 - y^2} dy \\
    =& R^4 \int_{-\frac \pi 2}^{\frac \pi 2} \sin^2 \theta \cos^2 \theta d\theta & \text{Letting } y = R \sin \theta \\
    =& \frac{R^4} 4 \int_{-\frac \pi 2}^{\frac \pi 2} \sin^2 2\theta \ d\theta & \sin 2\theta = 2 \sin \theta \cos \theta \\
    =& \frac{R^4} 4 \int_{-\frac \pi 2}^{\frac \pi 2} \frac {1 - \cos 4 \theta} 2 d \theta & \sin^2 \theta = \frac {1 - \cos 2 \theta} 2 \\
    =& \frac{R^4 \pi} 8 \\
\end{aligned}$$

Plug it into the original expression:

$$\begin{aligned}
    I =& \frac {2M} {\pi R^2} \int_{-R}^R y^2 \sqrt{R^2 - y^2} dy \\
    =& \frac {2M} {\pi R^2} \times \frac{R^4 \pi} 8 \\
    =& \boxed{\frac {MR^2} 4} \\
\end{aligned}$$

More practice: [here](https://zhuanlan.zhihu.com/p/466928586).

# Parallel Axis Theorem

$$\boxed{I_{\text{parallel axis}} = I_{CM} + M \times D^2}$$

## 💡 Proof

Assume that in a Cartesian coordinate system the perpendicular distance $D$ between the two axes lies on the x-axis and the center of mass lies on the origin.

$$\begin{aligned}
    & I_{\text{parallel axis}} \\
    =& \int ((x - D)^2 + y^2) dm \\
    =& \int (x^2 + y^2) dm - 2D \int x dm + \int D^2 dm \\
    =& I_{CM} - 2D (M x_{CM}) + M D^2 \\
    =& I_{CM} + M D^2 \\
\end{aligned}$$

- <https://en.wikipedia.org/wiki/Parallel_axis_theorem>

## Example 8.4

> In Example 8.1, it was found that the rotational inertia about the $z$-axis of a uniform rod of mass $M$ reaching from the origin along the $x$-axis to $x = L$ is $I = \frac {ML^2} 3$. Calculate the moment of inertia of the rod about an axis parallel to the $z$-axis passing through the middle of the rod.

$$\begin{aligned}
    & I_{CM} \\
    =& I_{\text{parallel axis}} - MD^2 \\
    =& \frac {ML^2} 3 - \frac {ML^2} 4 \\
    =& \boxed{\frac {ML^2} {12}} \\
\end{aligned}$$

# Assemblies of Piecewise Smooth Objects or Points

The rotational inertia of any assembly of of objects is the sum of the rotational inertias of the individual objects.

$$\boxed{I = I_{\text{object 1}} + I_{\text{object 2}}}$$

# Force $\to$ Torque

We are expecting a rotational analog of $\vec F = m \vec a$, so we start from the expression $I \alpha$:

$$\begin{aligned}
    & I \alpha \\
    =& \int r^2 \alpha dm \\
    =& \int r a_{\tan} dm \\
    =& \int r dF_{\tan} \\
    =& r \times F_{\tan} \\
\end{aligned}$$

Therefore, it is very natural to define torque $\tau$ as:

$$\tau = r F_{\tan} = r F \sin \theta$$

$$\boxed{\vec{\tau} = \vec{r} \times \vec{F}}$$

💡 It's a cross product, which means it is a pseudo-vector as well!

And we have the Newton's second law for rotational motion:

$$\boxed{\vec{\tau}_{\text{net}} = I \vec{\alpha}}$$

### 💡 From the perspective of pseudo-vectors

$$\begin{aligned}
    & I \vec{\alpha} \\
    =& \int r^2 \vec{\alpha} dm \\
    =& \int (\vec{r} \cdot \vec{r}) \vec{\alpha} dm \\
    =& \int ((\vec{r} \cdot \vec{r}) \vec{\alpha} - (\vec{r} \cdot \vec{\alpha}) \vec{r}) dm & \vec{r} \cdot \vec{\alpha} = 0 \\
    =& \int \vec{r} \times (\vec{\alpha} \times \vec{r}) dm & \text{Vector triple product} \\
    =& \int \vec{r} \times \vec{a}_{\tan} dm \\
    =& \int \vec{r} \times d\vec{F}_{\tan} \\
    =& \vec{r} \times \vec{F}_{\tan} \\
\end{aligned}$$

- Vector triple product $\vec{a} \times (\vec{b} \times \vec{c}) = (\vec{a} \cdot \vec{c})\vec{b} - (\vec{a} \cdot \vec{b}) \vec{c}$
- <https://pressbooks.online.ucf.edu/osuniversityphysics/chapter/10-7-newtons-second-law-for-rotation/>
- <https://en.wikipedia.org/wiki/Triple_product>

### Is torque is kind of energy?

The unit of torque is newton meters (which is the same as joule), but it doesn't mean that torque is a kind of energy.

> <https://physics.stackexchange.com/questions/37881/why-is-torque-not-measured-in-joules>
>
> Fun fact: alternative units for torque are Joules/radian, though not heavily used.

This can be shown in the following part.

## Work Done by an External Force

$$\begin{aligned}
    & dW \\
    =& \vec{F} \cdot d\vec{r} \\
    =& \vec{F}_{\tan} \cdot d\vec{r} \\
    =& F_{\tan} \cdot r \cdot d\theta \\
    =& \tau d\theta \\
\end{aligned}$$

We've got the expression of work in rotational systems:

$$\boxed{dW = \tau d\theta \Leftrightarrow W = \int \tau d\theta \xlongequal{\text{const } \tau} \tau \Delta \theta}$$

## Potential Energy

$$\begin{aligned}
    & \tau \\
    =& \frac {dW} {d\theta} \\
    =& \frac {dKE} {d\theta} \\
    =& -\frac {dU} {d\theta} \\
\end{aligned}$$

Using the above arguments, we can relate torque to potential energy (valid only if the torque is produced by **conservative forces**):

$$\boxed{\tau = - \frac {dU} {d\theta}}$$

## Power

$$\begin{aligned}
    & P \\
    =& \frac {dW} {dt} \\
    =& \tau \frac {d\theta} {dt} \\
    =& \tau \omega \\
\end{aligned}$$

Now we can relate power in rotational systems:

$$\boxed{P = \tau \omega}$$

# Momentum $\to$ Angular Momentum

We are expecting a rotational analog of $\vec P = m \vec v$, so we start from the expression $I \vec{\omega}$:

$$\begin{aligned}
    & I \vec{\omega} \\
    =& \int r^2 \vec{\omega} dm \\
    =& \int (\vec{r} \cdot \vec{r}) \vec{\omega} dm \\
    =& \int ((\vec{r} \cdot \vec{r}) \vec{\omega} - (\vec{r} \cdot \vec{\omega}) \vec{r}) dm & \vec{r} \cdot \vec{\omega} = 0 \\
    =& \int \vec{r} \times (\vec{\omega} \times \vec{r}) dm \\
    =& \int \vec{r} \times \vec{v} dm \\
    =& \int \vec{r} \times d\vec{p} \\
    =& \vec{r} \times \vec{p} \\
\end{aligned}$$

Therefore, it is very natural to define angular momentum $L$ as:

$$\boxed{\vec{L} = \vec{r} \times \vec{p}}$$

💡 It's a cross product, which means it is a pseudo-vector as well!

And we have the relationship between angular momentum and angular inertia:

$$\boxed{\vec{L} = I \vec{\omega}}$$

## Relationship Between Torque and Angular Momentum

$$\vec{\tau}_{\text{net}} = I \vec{\alpha} = I \frac {d\vec{\omega}} {dt} = \frac {d\vec{L}} {dt}$$

$$\boxed{\vec{\tau}_{\text{net}} = \frac {d\vec{L}} {dt}}$$

# ☆Conservation of Angular Momentum

$$\begin{aligned}
    \vec{L}_\text{net} &= \text{const} \\
    \frac {d\vec{L}} {dt} &= 0 \\
    \vec{\tau}_{\text{net}} &= 0 \\
\end{aligned}$$

> **If the net external torque acting on an object or system of objects is zero, the total angular momentum is constant.**

## Example 8.6

> (Page 220 & 221 of the book)
>
> A person is sitting on a rotating lab stool holding a top that is free to rotate, as shown in Figure 8.6. The top is initially pointing vertically and rotating counterclockwise (as viewed from above) so that its angular momentum vector of magnitude $L$ points in the $+z$-direction. The person turns the top (which continues to rotate about its axis with a constant speed) to a final angle $\theta$ as shown. If the person is initially at rest, what is the person's final angular velocity with respect to the laboratory? (The person-top system has a rotational inertia of $I$ about the $z$-axis)

$$\begin{aligned}
    L_{z,\text{before}} &= L_{z,\text{top,final}} + L_{z,\text{person,final}} \\
    L &= L \cos \theta + I \omega_{\text{person}} \\
    \omega_{\text{person}} &= \boxed{\frac {L (1 - \cos \theta)} I} \\
\end{aligned}$$
