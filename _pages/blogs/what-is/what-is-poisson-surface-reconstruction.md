---
title: What is Poisson Surface Reconstruction
permalink: /blogs/what-is-poisson-surface-reconstruction
medium: blog
category: what-is
---

## Introduction

**Poisson Surface Reconstruction (PSR)** is a widely used method in geometry processing for recovering a smooth watertight surface from a set of 3D points equipped with normals. Originally proposed by Kazhdan et al. (2006)[^1], PSR is robust to noise and outliers, making it a standard approach in 3D scanning, reverse engineering, and computer graphics.

---

## Core Idea

The method interprets surface reconstruction as a spatial inference problem:

* Given a set of oriented points (points + normals), we wish to reconstruct the implicit indicator function of the solid object.
* The gradient of this indicator function should align with the input normals.
* By formulating this alignment as a Poisson equation, solving it yields an implicit scalar function whose isosurface represents the reconstructed surface.

---

## The Poisson Equation

Given a point cloud with oriented normals $\{\mathbf{p}_i, \mathbf{n}_i\}$, we want to reconstruct a scalar indicator function $\chi: \Omega \subset \mathbb{R}^3 \to \mathbb{R}$ such that its **gradient approximates the normal field**.

Formally, we define a vector field $\mathbf{V}$ on $\Omega$ representing the normals, e.g., by extending the discrete normals to a continuous field using kernel smoothing. 

The Poisson formulation is then:

$$
\begin{equation}
\label{eq:poisson}
\nabla \cdot \nabla \chi = \nabla \cdot \mathbf{V} \quad \text{in } \Omega
\end{equation}
$$

* $\nabla \chi$ is the gradient of the implicit function (points in the direction of increasing $\chi$).
* $\nabla \cdot \nabla \chi = \Delta \chi$ is the Laplacian.
* $\nabla \cdot \mathbf{V}$ is the divergence of the input normal field.

subject to boundary conditions, e.g.:

* **Dirichlet boundary conditions**: $\phi=0$ on $\partial\Omega$
   - This specifies the value of the function $\phi$ at the boundary
   - $\partial\Omega$ represents the boundary of domain Omega

* **Neumann boundary conditions**: $\nabla \chi \cdot \mathbf{n}=0$ on $\partial\Omega$
   - This specifies the normal derivative at the boundary
   - $\mathbf{n}$ is the unit normal vector

---

## Weak Formulation

To solve numerically, we move from the **strong form** to a **weak (variational) form**. 

Remember integration by parts theorem for the familiar 1D version is defined as: 

$$
\int_a^b u''(x)\, v(x)\, dx
= \Big[ u'(x)v(x) \Big]_a^b - \int_a^b u'(x)\, v'(x)\, dx
$$

* The boundary term $[u'(x)v(x)]_a^b$ comes from the derivative transfer.
* This is what weakens the differentiability requirement: instead of needing $u$ twice differentiable, we only need $u$ once differentiable (since only $u'$ appears in the weak form).

For vector calculus, generalizing to higher dimensions, the theorem is called **divergence theorem**:

$$
\begin{equation}
\int_\Omega \nabla \cdot \mathbf{F} \, dV = \int_{\partial \Omega} \mathbf{F} \cdot \mathbf{n} \, dS
\end{equation}
$$

where:

* $\Omega$ is the domain,
* $\partial \Omega$ its boundary,
* $\mathbf{n}$ is the outward unit normal.

Use integration by parts on the left-hand side of $\eqref{eq:poisson}$:

$$
\Delta \chi = \nabla \cdot \nabla \chi
$$

Multiply by test function $\phi$ and integrate:

$$
\int_\Omega (\Delta \chi) \, \phi \, dV
= \int_\Omega (\nabla \cdot \nabla \chi)\, \phi \, dV
$$

Now set $\mathbf{F} = \phi \, \nabla \chi$.
Then:

$$
\nabla \cdot \mathbf{F} = \nabla \phi \cdot \nabla \chi + \phi \, \Delta \chi
$$

Integrating:

$$
\int_\Omega \nabla \cdot (\phi \nabla \chi)\, dV
= \int_\Omega \nabla \phi \cdot \nabla \chi \, dV + \int_\Omega \phi \, \Delta \chi \, dV
$$

Apply divergence theorem:

$$
\int_{\partial \Omega} (\phi \nabla \chi) \cdot \mathbf{n} \, dS
= \int_\Omega \nabla \phi \cdot \nabla \chi \, dV + \int_\Omega \phi \, \Delta \chi \, dV
$$

Rearrange:

$$
\int_\Omega \phi \, \Delta \chi \, dV
= - \int_\Omega \nabla \chi \cdot \nabla \phi \, dV
+ \int_{\partial \Omega} \phi \, (\nabla \chi \cdot \mathbf{n}) \, dS
$$

Considering the boundary conditions:

* If **Dirichlet boundary conditions** ($\phi=0$ on $\partial\Omega$), the boundary term vanishes.
* If **Neumann boundary conditions** ($\nabla \chi \cdot \mathbf{n}=0$ on $\partial\Omega$), it also vanishes.

So the simplified weak form becomes:

$$
\begin{equation}
\int_\Omega \phi \, \Delta \chi \, dV
= - \int_\Omega \nabla \chi \cdot \nabla \phi \, dV
\end{equation}
$$

Use integration by parts again on the right-hand side of $\eqref{eq:poisson}$:

$$
\int_{\Omega} (\nabla \cdot \mathbf{V}) \, \phi \, dV = - \int_{\Omega} \mathbf{V} \cdot \nabla \phi \, dV + \int_{\partial \Omega} (\mathbf{V} \cdot \mathbf{n}) \phi \, dS
$$

Boundary term again vanishes:

$$
\begin{equation}
\int_{\Omega} (\nabla \cdot \mathbf{V}) \, \phi \, dV = - \int_{\Omega} \mathbf{V} \cdot \nabla \phi \, dV
\end{equation}
$$

Combine the derivations from both sides:

$$
\begin{equation}
\int_\Omega \nabla \chi \cdot \nabla \phi \, d\Omega = \int_\Omega \mathbf{V} \cdot \nabla \phi \, d\Omega, \quad \forall \phi
\end{equation}
$$

This expresses the problem as finding $\chi \in H^1(\Omega)$ such that the inner product of its gradient with test functions equals the inner product of the input vector field with the gradients of test functions.

---

## Basis Functions and Discretization

To solve numerically, we approximate $\chi$ using a finite set of **basis functions** $\{\phi_j\}_{j=1}^N$:

$$
\begin{equation}
\chi(x) \approx \sum_{j=1}^N \alpha_j \phi_j(x)
\end{equation}
$$

* In PSR, $\phi_j$ are **piecewise polynomial B-splines** defined on octree nodes.
* In 1D, a quadratic B-spline $B^2(x)$ is defined piecewise:

$$
\begin{equation}
B^2(x) =
\begin{cases}
\frac{1}{2} x^2, & 0 \le x < 1 \\
-\frac{1}{2}(x-2)^2 + 2, & 1 \le x < 2 \\
0, & \text{otherwise}
\end{cases}
\end{equation}
$$

* In 3D, we use **tensor products**:

$$
\begin{equation}
\phi_{i,j,k}(x,y,z) = B^2(x - x_i) \, B^2(y - y_j) \, B^2(z - z_k)
\end{equation}
$$

The compact support ensures sparsity in the resulting system matrix.

Substitute the expansion into the weak form:

$$
\int_\Omega \nabla \Big(\sum_j \alpha_j \phi_j \Big) \cdot \nabla \phi_i \, d\Omega = \int_\Omega \mathbf{V} \cdot \nabla \phi_i \, d\Omega, \quad i=1,\dots,N
$$

Which leads to a **linear system**:

$$
\begin{equation}
A \boldsymbol{\alpha} = \mathbf{b}, \quad A_{ij} = \int_\Omega \nabla \phi_j \cdot \nabla \phi_i \, d\Omega, \quad b_i = \int_\Omega \mathbf{V} \cdot \nabla \phi_i \, d\Omega
\end{equation}
$$

---

## Quadrature and Numerical Integration

Since exact integrals are intractable, PSR uses **numerical quadrature**:

$$
\begin{equation}
\int_\Omega f(x) \, d\Omega \approx \sum_{q=1}^Q w_q \, f(x_q)
\end{equation}
$$

* $x_q$: **quadrature points** (sample locations in each octree cell).
* $w_q$: **weights**, often related to the cell volume.

Applied to the system entries:

$$
\begin{equation}
A_{ij} \approx \sum_q w_q \, \nabla \phi_j(x_q) \cdot \nabla \phi_i(x_q), \quad b_i \approx \sum_q w_q \, \mathbf{V}(x_q) \cdot \nabla \phi_i(x_q)
\end{equation}
$$

This reduces continuous integrals into a **finite sum** suitable for sparse linear algebra.

---

## Numerical Solution

* The system $A \boldsymbol{\alpha} = \mathbf{b}$ is **symmetric positive definite**.
* Solved using iterative solvers, typically **Conjugate Gradient** or **Multigrid Preconditioned CG** for efficiency.
* Once solved, the coefficients $\alpha_j$ define the **implicit function**:

$$
\chi(x) = \sum_j \alpha_j \phi_j(x)
$$

* The final surface is extracted via **isosurface extraction**, e.g., Marching Cubes.
* Additional **vertex densities** can be computed to trim unreliable regions of the mesh.

---

[^1]: Kazhdan, M., Bolitho, M., & Hoppe, H. (2006). "Poisson Surface Reconstruction." In Proceedings of the Fourth Eurographics Symposium on Geometry Processing, pp. 61–70. [https://www.cs.jhu.edu/~misha/Code/PoissonRecon/](https://www.cs.jhu.edu/~misha/Code/PoissonRecon/)