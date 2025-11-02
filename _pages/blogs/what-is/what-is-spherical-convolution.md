---
title: What is Spherical Convolution
permalink: /blogs/what-is-spherical-convolution
medium: blog
category: what-is
tags:
  - geometry
---

## Formal Definitions

### Standard Spherical Convolution

For functions $f, \psi: S^2 \to \mathbb{R}$ and rotation $R \in SO(3)$:

$$
(f * \psi)(R) = \int_{S^2} f(\mathbf{x}) \psi(R^{-1} \mathbf{x})  d\mathbf{x}
$$

Where:

- $\mathbf{x} \in S^2$ is a point on the sphere
- $R^{-1} \mathbf{x}$ rotates the point $\mathbf{x}$ by $R^{-1}$
- $d\mathbf{x} = \sin\theta d\theta d\phi$ is the surface element

### Equivariant Formulation

More commonly, spherical convolution is defined as:

$$
(f * \psi)(R) = \int_{SO(3)} f(\mathbf{x}) \psi(R^{-1} \mathbf{x})  d\mathbf{x}
$$

But since $SO(3)$ acts transitively on $S^2$, this is equivalent to integrating over the sphere.

## Key Properties

### Rotation Equivariance

The most important property:

$$
[L_R f] *\psi = L_R [f* \psi]
$$

Where $L_R$ is the rotation operator: $L_R f(\mathbf{x}) = f(R^{-1} \mathbf{x})$

This means: **Rotating the input is equivalent to rotating the output**

### Non-commutativity

Unlike classical convolution, spherical convolution is generally non-commutative:

$$
f *\psi \neq \psi* f
$$

Due to the non-commutative nature of 3D rotations.

## Implementation Approaches

Using spherical harmonics, convolution becomes pointwise multiplication in the spectral domain:

**Spherical Harmonic Transform:**
$$
f_l^m = \int_{S^2} f(\mathbf{x}) Y_l^{m*}(\mathbf{x}) d\mathbf{x}
$$

**Spectral Convolution Theorem:**
$$
(f * \psi)_l^m = \sqrt{\frac{4\pi}{2l+1}} f_l^m \psi_l^0
$$

For more general filters:

$$
(f * \psi)(R) = \sum_{l=0}^{\infty} \sum_{m,m'=-l}^{l} f_l^m \psi_l^{m'} D^{(l)}_{mm'}(R)
$$

Where $D^{(l)}_{mm'}$ are Wigner D-matrices.
