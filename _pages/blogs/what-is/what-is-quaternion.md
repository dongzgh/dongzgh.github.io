---
title: What is Quaternion
permalink: /blogs/what-is-quaternion
medium: blog
category: what-is
tags:
  - geometry
---

## Gimbal Lock

Imagine you're using a camera stabilizer (a gimbal) that has three rings, one for each axis: **Pitch** (tilting up/down), **Yaw** (turning left/right), and **Roll** (tilting side to side).

**Gimbal lock occurs when one of these rings gets rotated to a point where the other two rings align.** Once they align, they are both trying to make the same rotation, and you suddenly **lose a degree of freedom**. You can no longer move in one independent direction.

## Quaternion

A quaternion is a 4-dimensional number system used to represent 3D rotations without gimbal lock. It is defined as:

$$
\mathbf{q} = a + b\mathbf{i} + c\mathbf{j} + d\mathbf{k}
$$

where $a, b, c, d$ are real numbers, and $\mathbf{i}, \mathbf{j}, \mathbf{k}$ are fundamental units. A rotation is represented by a **unit quaternion** ($\|\mathbf{q}\| = 1$), encoding a rotation of angle $θ$ around a unit axis $\mathbf{u} = (x, y, z)$ as:

$$
\mathbf{q} = [cos(θ/2), sin(θ/2)\mathbf{u}] = cos(θ/2) + sin(θ/2)(x\mathbf{i} + y\mathbf{j} + z\mathbf{k})
$$

It represents a rotation as a single rotation around an arbitrary axis, rather than three separate rotations around the $X$, $Y$, and $Z$ axes.

## Quaternion Algebra

The algebra is defined by the multiplication rules of the basis elements $\mathbf{i}, \mathbf{j}, \mathbf{k}$:

$$
\mathbf{i}^2 = \mathbf{j}^2 = \mathbf{k}^2 = \mathbf{i}\mathbf{j}\mathbf{k} = -1
$$

$$
\begin{array}{l}
\mathbf{i}\mathbf{j} = \mathbf{k},  \mathbf{j}\mathbf{i} = -\mathbf{k}\\
\mathbf{j}\mathbf{k} = \mathbf{\mathbf{i}},  \mathbf{k}\mathbf{j} = -\mathbf{\mathbf{i}}\\
\mathbf{k}\mathbf{i} = \mathbf{j},  \mathbf{i}\mathbf{k} = -\mathbf{j}\\
\end{array}
$$

Multiplication of two quaternions $\mathbf{q_1} = a + b\mathbf{i} + c\mathbf{j} + d\mathbf{k}$ and $\mathbf{q_2} = e + f\mathbf{i} + g\mathbf{j} + h\mathbf{k}$ is given by:

$$
\mathbf{q_1}\mathbf{q_2} = (ae - bf - cg - dh) + (af + be + ch - dg)\mathbf{i} + (ag - bh + ce + df)\mathbf{j} + (ah + bg - cf + de)\mathbf{k}
$$

**Key Property:** Quaternion multiplication is **non-commutative** ($\mathbf{q_1}\mathbf{q_2} ≠ \mathbf{q_2}\mathbf{q_1}$).

## Convert Euler Angles to Quaternion

For a common rotation order ($ZYX$: Yaw $ψ$, Pitch $θ$, Roll $φ$), the quaternion $\mathbf{q} = [a, b, c, d]$ is:

$$
\begin{array}{l}
a = cr*cp*cy + sr*sp*sy\\
b = sr*cp*cy - cr*sp*sy\\
c = cr*sp*cy + sr*cp*sy\\
d = cr*cp*sy - sr*sp*cy\\
\end{array}
$$

where:
* $cr = cos(φ/2)$, $sr = sin(φ/2)$ (Roll)
* $cp = cos(θ/2)$, $sp = sin(θ/2)$ (Pitch)
* $cy = cos(ψ/2)$, $sy = sin(ψ/2)$ (Yaw)

## Use Quaternion to for Rotations

To rotate a 3D point $\mathbf{p} = [x, y, z]$ by a unit quaternion $\mathbf{q}$, use the **sandwich product**:
1.  Represent the point as a pure quaternion: $\mathbf{v} = [0, x, y, z]$
2.  Calculate the inverse quaternion (for a unit quaternion, this is the conjugate): $\mathbf{q}^{-1} = [w, -i, -j, -k]$
3.  Apply the rotation: $\mathbf{v}^\prime = \mathbf{q} \mathbf{v} \mathbf{q}^{-1}$
The result $\mathbf{v}^\prime $ will be a pure quaternion $\mathbf{v}^\prime = [0, x^\prime, y^\prime, z^\prime]$, where $x^\prime, y^\prime, z^\prime$ are the coordinates of the rotated point. This operation is equivalent to rotating the point by angle $θ$ around axis $\mathbf{u}$.
