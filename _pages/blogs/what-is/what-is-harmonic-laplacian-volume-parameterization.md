---
title: What is Harmonic/Laplacian Volume Parameterization
permalink: /blogs/what-is-harmonic-laplacian-volume-parameterization
medium: blog
category: what-is
tags: 
  - geometry
---


## Overview

The main idea is to define a **smooth mapping** from a 3D volume $\Omega \subset \mathbb{R}^3$ to a parametric domain $\Omega' \subset \mathbb{R}^3$ (usually a cube) by solving **Laplace’s equation** with boundary constraints.

We want a function:

$$
\begin{equation}
\mathbf{u}(\mathbf{x}) = (u(\mathbf{x}), v(\mathbf{x}), w(\mathbf{x})) : \Omega \rightarrow \Omega'
\end{equation}
$$

where $u, v, w$ are the parametric coordinates, and $\mathbf{x} = (x,y,z)$ is a point inside the volume.

---

## Strong Formation

A **harmonic function** $u(\mathbf{x})$ is a scalar function that satisfies **Laplace’s equation**:

$$
\begin{equation}
\Delta u = 0
\end{equation}
$$

where the Laplacian operator $\Delta$ in 3D Cartesian coordinates is:

$$
\Delta u = \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} + \frac{\partial^2 u}{\partial z^2}
$$

* Here, $\mathbf{x} = (x, y, z)$ is a point inside the volume $\Omega$.
* Intuitively, at any point inside the domain, the value of $u$ is equal to the **average of its neighbors**, which is why harmonic functions are smooth and “no local extrema occur inside the domain.”

In volumetric parameterization, we don’t just have one scalar $u$; we have three parametric coordinates:

$$
\mathbf{u}(\mathbf{x}) = (u(\mathbf{x}), v(\mathbf{x}), w(\mathbf{x}))
$$

We impose the **harmonic condition** **component-wise**:

$$
\begin{equation}
\label{eq:strong-formation-1}
\Delta u = 0, \quad \Delta v = 0, \quad \Delta w = 0 \quad \text{in } \Omega
\end{equation}
$$

* Each of $u, v, w$ is a harmonic function inside the volume.
* This ensures that the resulting mapping $\mathbf{u}(\mathbf{x})$ is **smooth throughout the volume**.

The Laplace equation minimizes the **second derivatives**, i.e., the curvature, inside the domain.

Think of $\mathbf{u}$ as a **rubber sheet stretched over the boundary mapping**:

  * Fixed at the boundary (Dirichlet boundary conditions).
  * Interior points naturally settle into positions that minimize “tension.”

Formally, harmonic functions minimize the **Dirichlet energy**:

$$
\begin{equation}
E[\mathbf{u}] = \frac{1}{2} \int_\Omega \|\nabla \mathbf{u}\|^2 \, d\Omega
\end{equation}
$$

Minimizing this energy → smooth mapping, no unnecessary stretching.

The boundary condition is defined as:

$$
\begin{equation}
\label{eq:strong-formation-2}
\mathbf{u}(\mathbf{x}) = \mathbf{u}_\text{boundary}(\mathbf{x}), \quad \mathbf{x} \in \partial \Omega
\end{equation}
$$

Here:

* $\mathbf{u}_\text{boundary}$ defines how the boundary surface maps to the parametric domain (often a cube or other regular shape).

$\eqref{eq:strong-formation-1}$ and $\eqref{eq:strong-formation-2}$ are called the **strong form** because it requires the solution to satisfy the PDE **pointwise**.

---

## Weak Formulation

For numerical solutions, we often use the **weak form** (variational formulation).

First, inIntroduce a **test function** $\phi(\mathbf{x})$ that vanishes on the boundary:

$$
\begin{equation}
\phi(\mathbf{x}) = 0 \quad \text{for } \mathbf{x} \in \partial \Omega
\end{equation}
$$

Multiply the PDE by $\phi$ and integrate over the volume:

$$
\int_\Omega (\Delta u) \, \phi \, d\Omega = 0
$$

We want to reduce the order of derivatives on $u$ (from second to first order) because that allows **FEM discretization**. Using **integration by parts**:

$$
\int_\Omega (\Delta u) \, \phi \, d\Omega = \int_\Omega \nabla \cdot (\nabla u) \, \phi \, d\Omega
$$

Apply the **divergence theorem**:

$$
\int_\Omega \nabla \cdot (\phi \nabla u) \, d\Omega = \int_\Omega \nabla \phi \cdot \nabla u \, d\Omega + \int_\Omega \phi \Delta u \, d\Omega
$$

Rewriting:

$$
\int_\Omega \phi \, \Delta u \, d\Omega = \int_{\partial \Omega} \phi (\nabla u \cdot \mathbf{n}) \, dS - \int_\Omega \nabla u \cdot \nabla \phi \, d\Omega
$$

* $\mathbf{n}$ = outward normal at boundary
* $dS$ = surface element

Since $\phi = 0$ on the boundary (Dirichlet BC), the surface term vanishes:

$$
\int_{\partial \Omega} \phi (\nabla u \cdot \mathbf{n}) \, dS = 0
$$

Thus, we get the **weak form**:

$$
\begin{equation}
\boxed{\int_\Omega \nabla u \cdot \nabla \phi \, d\Omega = 0 \quad \forall \phi \in H_0^1(\Omega)}
\end{equation}
$$

* $H^1(\Omega)$ is the Sobolev space of functions with square-integrable derivatives.
* $\phi$ is a test function vanishing on the boundary ($H_0^1$).

---

## Discretization

Subdivide $\Omega$ into small **elements**, usually tetrahedra for irregular 3D volumes.

* Let $V = \{v_1, v_2, \dots, v_n\}$ be the **vertices** of the mesh.
* Let $T = \{t_1, t_2, \dots, t_m\}$ be the **tetrahedral elements**.

Represent $u$ as a **linear combination of basis functions** $\phi_i(\mathbf{x})$:

$$
\begin{equation}
u(\mathbf{x}) \approx \sum_{i=1}^{n} u_i \phi_i(\mathbf{x})
\end{equation}
$$

* $u_i$ = unknown value at vertex $i$
* $\phi_i$ = “hat” function: $\phi_i(v_j) = \delta_{ij}$, linear within each tetrahedron

Similarly, approximate test functions $\phi$ using the same basis functions:

$$
\begin{equation}
\phi = \phi_j \quad \text{for each vertex } j
\end{equation}
$$

Substitute $u(\mathbf{x}) = \sum_i u_i \phi_i$ and $\phi = \phi_j$ into the weak form:

$$
\int_\Omega \nabla \left(\sum_i u_i \phi_i\right) \cdot \nabla \phi_j \, d\Omega = 0
$$

Simplify:

$$
\sum_i u_i \int_\Omega \nabla \phi_i \cdot \nabla \phi_j \, d\Omega = 0
$$

* This is a **linear system**:

$$
\begin{equation}
\mathbf{L} \mathbf{u} = \mathbf{0}
\end{equation}
$$

* $\mathbf{L}$ = **stiffness matrix**, where $L_{ij} = \int_\Omega \nabla \phi_i \cdot \nabla \phi_j \, d\Omega$

For each tetrahedron $t$ with vertices $i,j,k,l$:

$$
\begin{equation}
L^t_{mn} = \int_{t} \nabla \phi_m \cdot \nabla \phi_n \, d\Omega
\end{equation}
$$

For **linear tetrahedra**, $\nabla \phi_m$ is constant inside $t$, integral reduces to:

$$
\begin{equation}
L^t_{mn} = (\nabla \phi_m \cdot \nabla \phi_n) \cdot \text{Vol}(t)
\end{equation}
$$

Assemble all local contributions into the **global sparse stiffness matrix** $\mathbf{L}$.

Partition vertices into **interior** and **boundary**:

$$
\begin{equation}
\mathbf{u} = 
\begin{bmatrix}
\mathbf{u}_\text{interior} \\
\mathbf{u}_\text{boundary}
\end{bmatrix}
\end{equation}
$$

Rewrite linear system:

$$
\mathbf{L}_{II} \mathbf{u}_\text{interior} + \mathbf{L}_{IB} \mathbf{u}_\text{boundary} = 0
$$

Solve for interior vertices:

$$
\begin{equation}
\mathbf{u}_\text{interior} = - \mathbf{L}_{II}^{-1} \mathbf{L}_{IB} \mathbf{u}_\text{boundary}
\end{equation}
$$

* Use **direct solvers** (sparse LU/Cholesky) for small meshes.
* Use **iterative solvers** (Conjugate Gradient, Multigrid) for large meshes.

Repeat for $v$ and $w$ components to get full volumetric mapping:

$$
\mathbf{u}(\mathbf{x}) = (u(\mathbf{x}), v(\mathbf{x}), w(\mathbf{x}))
$$

---

## Summary

1. **Mesh the volume** into tetrahedra.
2. **Define boundary mapping** $u_\text{boundary}$.
3. **Choose basis functions** (linear “hat” functions).
4. **Assemble stiffness matrix** $L$ from $\int \nabla \phi_i \cdot \nabla \phi_j$.
5. **Apply boundary conditions** and separate interior vs boundary vertices.
6. **Solve the linear system** for interior vertices.
7. **Repeat for all parametric components** $u,v,w$.

---

## Appendix

### Hat Function

Consider a tetrahedron $T$ with vertices $v_1, v_2, v_3, v_4$.
We want linear basis functions $\phi_1, \phi_2, \phi_3, \phi_4$ inside $T$ such that:

$$
\phi_i(v_j) = \delta_{ij}, \quad i,j = 1,2,3,4
$$

* **Linear in space**: $\phi_i(\mathbf{x}) = a_i x + b_i y + c_i z + d_i$
* Solve a **linear system** to satisfy the nodal values:

$$
\begin{bmatrix}
x_1 & y_1 & z_1 & 1 \\
x_2 & y_2 & z_2 & 1 \\
x_3 & y_3 & z_3 & 1 \\
x_4 & y_4 & z_4 & 1
\end{bmatrix}
\begin{bmatrix}
a_i \\ b_i \\ c_i \\ d_i
\end{bmatrix}
=
\begin{bmatrix}
\delta_{i1} \\ \delta_{i2} \\ \delta_{i3} \\ \delta_{i4}
\end{bmatrix}
$$

* Solve for $a_i, b_i, c_i, d_i$ → defines the **linear hat function** in $T$.
* Repeat for all tetrahedra.

Linear Hat Function has the following properties:

| Property               | Description                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------- |
| **Local support**      | $\phi_i(\mathbf{x}) \neq 0$ only in tetrahedra containing vertex $i$                  |
| **Partition of unity** | $\sum_{i=1}^4 \phi_i(\mathbf{x}) = 1$ inside each tetrahedron                         |
| **Linear gradient**    | $\nabla \phi_i$ is **constant inside each tetrahedron** → simplifies stiffness matrix |
| **Continuity**         | $\phi_i$ is continuous across tetrahedra (C0 continuity)                              |
| **Sparse stiffness**   | Only neighboring vertices interact in $\int \nabla \phi_i \cdot \nabla \phi_j$        |

### Variational (Energy Minimization)

The **Dirichlet energy** measures the “roughness” of a function $u(\mathbf{x})$ inside a volume $\Omega$:

$$
E[u] = \frac{1}{2} \int_\Omega \|\nabla u(\mathbf{x})\|^2 \, d\Omega
$$

* $\nabla u = (\partial u/\partial x, \partial u/\partial y, \partial u/\partial z)$
* $\|\nabla u\|^2 = (\partial u/\partial x)^2 + (\partial u/\partial y)^2 + (\partial u/\partial z)^2$

**Goal:** Find $u$ that **minimizes** $E[u]$ subject to boundary conditions:

$$
u(\mathbf{x}) = u_\text{boundary}(\mathbf{x}) \quad \text{on } \partial \Omega
$$

Intuition: This gives the **smoothest mapping** of interior points given fixed boundaries.

Consider a small variation in $u$:

$$
u \to u + \epsilon \phi
$$

* $\phi(\mathbf{x})$ = arbitrary **test function** vanishing on the boundary ($\phi|_{\partial \Omega} = 0$)
* $\epsilon$ = small scalar parameter

Compute the energy for the perturbed function:

$$
E[u + \epsilon \phi] = \frac{1}{2} \int_\Omega \|\nabla (u + \epsilon \phi)\|^2 \, d\Omega
$$

$$
\nabla (u + \epsilon \phi) = \nabla u + \epsilon \nabla \phi
$$

$$
\|\nabla (u + \epsilon \phi)\|^2 = \|\nabla u\|^2 + 2 \epsilon (\nabla u \cdot \nabla \phi) + \epsilon^2 \|\nabla \phi\|^2
$$

Substitute into the energy:

$$
E[u + \epsilon \phi] = \frac{1}{2} \int_\Omega \|\nabla u\|^2 + 2 \epsilon (\nabla u \cdot \nabla \phi) + \epsilon^2 \|\nabla \phi\|^2 \, d\Omega
$$

$$
E[u + \epsilon \phi] = E[u] + \epsilon \int_\Omega \nabla u \cdot \nabla \phi \, d\Omega + \frac{\epsilon^2}{2} \int_\Omega \|\nabla \phi\|^2 \, d\Omega
$$


For $u$ to **minimize the energy**, the derivative of $E$ with respect to $\epsilon$ at $\epsilon = 0$ must vanish:

$$
\frac{d}{d\epsilon} E[u + \epsilon \phi] \Big|_{\epsilon=0} = \int_\Omega \nabla u \cdot \nabla \phi \, d\Omega = 0
$$

* This must hold for **all test functions** $\phi$ vanishing on the boundary.

The condition:

$$
\int_\Omega \nabla u \cdot \nabla \phi \, d\Omega = 0 \quad \forall \phi \in H_0^1(\Omega)
$$

is exactly the **weak (variational) form** of Laplace’s equation, so the **weak form is derived directly from energy minimization**.
