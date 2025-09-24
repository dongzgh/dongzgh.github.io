---
title: What is Eigenfunction-based Spherical Parameterization
permalink: /blogs/what-is-eigenfunction-based-spherical-parameterization
medium: blog
category: what-is
---

## Overview

On a Riemannian surface $\mathcal{M}$ (with area measure $dA$) the Laplace–Beltrami eigenproblem is defined as:

$$
\begin{equation}
-\Delta_{\mathcal M} u = \lambda u \quad\text{on }\mathcal{M},
\end{equation}
$$

together with boundary conditions if $\partial\mathcal M\neq\varnothing$ (often we consider a closed surface so $\partial\mathcal M=\varnothing$).
Here $\Delta_{\mathcal M}=\nabla_{\mathcal M}\cdot\nabla_{\mathcal M}$ is the surface divergence of the surface gradient.

Solving this eigenproblem yields **harmonic modes** or **vibration modes** $(\lambda_i, u_i)$ of the shape.

## Weak Formulation

Choose a test function $v$ from a suitable space of functions (typically $v\in C^\infty(\mathcal M)$ or more generally $v\in H^1(\mathcal M)$). Multiply the strong equation by $v$ and integrate over the surface:

$$
\int_{\mathcal M} \big(-\Delta_{\mathcal M} u\big)\, v \; dA \;=\; \int_{\mathcal M} \lambda u\, v \; dA.
$$

Use the surface divergence theorem / integration by parts theorem (valid for any tangent vector field $X$):

$$
\begin{equation}
\int_{\mathcal M} (\nabla_{\mathcal M}\cdot X)\, v \, dA
= -\int_{\mathcal M} X\cdot \nabla_{\mathcal M} v \, dA
\;+\; \int_{\partial\mathcal M} v\,(X\cdot n)\, ds,
\end{equation}
$$

Set $X=\nabla_{\mathcal M} u$. Then

$$
\int_{\mathcal M} -(\Delta_{\mathcal M} u)\, v \, dA
= \int_{\mathcal M} \nabla_{\mathcal M} u \cdot \nabla_{\mathcal M} v \, dA
\;-\; \int_{\partial\mathcal M} v\,(\partial_n u)\, ds,
$$

where $\partial_n u = \nabla_{\mathcal M}u\cdot n$ is the normal derivative along the boundary curve (here $n$ is the outward unit co-normal to $\partial\mathcal M$ lying in the tangent plane of $\mathcal M$).

Considering the following boundary conditions:

* **Closed surface** ($\partial\mathcal M=\varnothing$): the boundary term vanishes automatically.
* **Dirichlet boundary**: if $u$ is fixed on $\partial\mathcal M$ we restrict test functions $v$ to vanish on $\partial\mathcal M$, so the boundary term is zero.
* **Neumann boundary**: if $\partial_n u=0$ (natural BC) the boundary term is zero as well.

Assuming the boundary term vanishes (closed surface or appropriate conditions), we obtain the weak form:

$$
\begin{equation}
\boxed{\;\int_{\mathcal M} \nabla_{\mathcal M} u \cdot \nabla_{\mathcal M} v \; dA \;=\; \lambda \int_{\mathcal M} u\, v \; dA \quad\forall v\in H^1(\mathcal M)\;. \;}
\end{equation}
$$

This is the variational (weak) formulation of the eigenproblem.

* The weak form lives in the Sobolev space $H^1(\mathcal M)$ (functions with square-integrable value and surface gradient).
* The left bilinear form $a(u,v)=\int \nabla_{\mathcal M}u\cdot\nabla_{\mathcal M}v\,dA$ is symmetric, continuous and (on connected compact $\mathcal M$) positive semidefinite.
* The right form $b(u,v)=\int u v\,dA$ is the mass inner product. Standard theory (Rayleigh quotient, spectral theorem) yields a discrete set of real eigenvalues and orthogonal eigenfunctions.

---

## Discretization

Choose a finite-dimensional subspace spanned by basis functions $\{\phi_1,\dots,\phi_n\}$ (e.g. piecewise-linear hat functions on a triangulated mesh). Seek $u$ of the form

$$
u = \sum_{i=1}^n u_i \phi_i,\qquad v=\phi_j.
$$

Plug into the weak form (for every basis index $j$):

$$
\sum_{i=1}^n u_i \int_{\mathcal M} \nabla_{\mathcal M}\phi_i\cdot\nabla_{\mathcal M}\phi_j \, dA
= \lambda \sum_{i=1}^n u_i \int_{\mathcal M} \phi_i\phi_j \, dA.
$$

Define stiffness and mass matrices

$$
\begin{equation}
L_{ji} := \int_{\mathcal M} \nabla_{\mathcal M}\phi_i\cdot\nabla_{\mathcal M}\phi_j \, dA,\qquad
M_{ji} := \int_{\mathcal M} \phi_i\phi_j \, dA.
\end{equation}
$$

In matrix form:

$$
\begin{equation}
L\mathbf{u} = \lambda\, M\mathbf{u},
\end{equation}
$$

the standard **generalized eigenproblem**.

### Hat Function

For a triangulated surface mesh with vertices $\{p_1, p_2, \dots, p_n\}$, the hat function $\phi_i$ associated with vertex $p_i$ is defined by:

$$
\begin{equation}
\phi_i(p_j) = \begin{cases}
1, & j=i, \\
0, & j\neq i.
\end{cases}
\end{equation}
$$

and it is **piecewise linear** over each triangle.

That means:

* $\phi_i$ is **supported only on the 1-ring neighborhood** of $p_i$ (the union of triangles incident to $p_i$).
* On each incident triangle, $\phi_i$ is an affine function that interpolates values at its three vertices.

Take a triangle $T = (p_i, p_j, p_k)$.
Define **barycentric coordinates** $(\lambda_i, \lambda_j, \lambda_k)$ for any point $x\in T$ such that:

$$
\begin{equation}
x = \lambda_i p_i + \lambda_j p_j + \lambda_k p_k, \quad
\lambda_i+\lambda_j+\lambda_k = 1, \quad \lambda_i,\lambda_j,\lambda_k \geq 0.
\end{equation}
$$

Then:

$$
\begin{equation}
\phi_i|_T(x) = \lambda_i(x)
\end{equation}
$$

$$
\begin{equation}
\phi_j|_T(x) = \lambda_j(x)
\end{equation}
$$

$$
\begin{equation}
\phi_k|_T(x) = \lambda_k(x)
\end{equation}
$$

So the **hat function = barycentric coordinate**.

### Stiffness Matrix

Since barycentric coordinates are affine, their gradients are constant over each triangle.
For vertex $i$ in triangle $(i,j,k)$:

$$
\begin{equation}
\nabla \phi_i = \frac{n \times (p_k - p_j)}{2A_T},
\end{equation}
$$

where

* $n$ = unit normal of the triangle,
* $A_T$ = triangle area.

This formula ensures:

* $\nabla \phi_i$ is orthogonal to edge $(j,k)$,
* magnitude is $1/height$ of the triangle.

This constant gradient is what gives the **cotangent weights** when you assemble the stiffness matrix.

For vertices $i$ and $j$, restricted to this triangle:

$$
\nabla \phi_i \cdot \nabla \phi_j
= \frac{1}{(2 A_T)^2}\big[(n \times (p_k - p_j)) \cdot (n \times (p_i - p_k))\big].
$$

Use the vector triple product identity:

$$
\begin{equation}
(a \times n)\cdot (b \times n) = (a \cdot b)(n \cdot n) - (a\cdot n)(b\cdot n).
\end{equation}
$$

Since both $p_k-p_j$ and $p_i-p_k$ lie in the triangle plane, they’re orthogonal to $n$. So:

$$
(n \times (p_k - p_j))\cdot(n \times (p_i - p_k)) 
= (p_k - p_j)\cdot(p_i - p_k).
$$

Thus:

$$
\begin{equation}
\nabla \phi_i \cdot \nabla \phi_j = \frac{(p_k - p_j)\cdot(p_i - p_k)}{(2A_T)^2}.
\end{equation}
$$

Look at the angle at vertex $k$ (opposite edge $(i,j)$).

* Numerator: $(p_k - p_j)\cdot(p_i - p_k) = \|p_k-p_j\|\,\|p_i-p_k\|\cos\theta_k$.
* Denominator: $(2A_T)^2 = \| (p_j-p_i)\times(p_k-p_i)\|^2 = (\|p_j-pi\|\|p_k-pi\|\sin\theta_k)^2$.

Simplify:

$$
\begin{equation}
\nabla \phi_i \cdot \nabla \phi_j
= -\frac{1}{4A_T}\cot\theta_k.
\end{equation}
$$

That minus sign appears naturally depending on ordering; the standard convention gives:

$$
\begin{equation}
L_{ij}\big|_T = -\tfrac{1}{2}\cot\theta_k.
\end{equation}
$$

Summing over all triangles incident to edge $(i,j)$:

$$
\begin{equation}
L_{ij} = -\tfrac{1}{2}(\cot \alpha + \cot \beta),
\end{equation}
$$

where $\alpha,\beta$ are the two angles opposite edge $(i,j)$.

### Mass Matrix

We need the integrals

$$
\int_T \lambda_a \lambda_b \, dA \quad\text{for } a,b\in\{1,2,3\}.
$$

Known exact results (standard barycentric integrals):

* Diagonal (same index):

  $$
  \begin{equation}
  \int_T \lambda_a^2 \, dA \;=\; \frac{A_T}{6}.
  \end{equation}
  $$
* Off-diagonal (different indices):

  $$
  \begin{equation}
  \int_T \lambda_a \lambda_b \, dA \;=\; \frac{A_T}{12},\quad a\ne b.
  \end{equation}
  $$

(You can derive these by mapping $T$ to a reference triangle and integrating monomials in barycentric coordinates, or using symmetry and the identity $\int_T (\lambda_1+\lambda_2+\lambda_3)^2 dA = A_T$.)

Thus the local $3\times3$ mass matrix for triangle $T$ with vertex order (1,2,3) is:

$$
\begin{equation}
M^T \;=\; \frac{A_T}{12}
\begin{bmatrix}
2 & 1 & 1\\[4pt]
1 & 2 & 1\\[4pt]
1 & 1 & 2
\end{bmatrix}.
\end{equation}
$$

Check: diagonal entries are $A_T/6$, off-diagonals $A_T/12$. This is symmetric and positive definite.

To build the global consistent mass matrix $M$ of size $n\times n$:

* For each triangle $T$ with vertices indices $(i,j,k)$ and area $A_T$, add the local block $M^T$ into the global matrix positions $(i,j,k)$ — i.e.

  * $M_{ii} += A_T/6$,
  * $M_{ij} += A_T/12$, etc.

After processing all triangles you obtain the full sparse symmetric matrix $M$.

## Solution

Solving the eigenfunction to obtain non-trivial eigenvalue-eigenvector pairs $(\lambda_i, u_i)$.

For each vertex $i$ form the 3D vector

$$
\begin{equation}
r_i = \big(u_1(i),\; u_2(i),\; u_3(i)\big).
\end{equation}
$$

Then normalize

$$
\begin{equation}
u_i = \frac{r_i}{\|r_i\|}.
\end{equation}
$$

Handle numerical issues: if $\|r_i\|$ is below a tiny tolerance (rare), perturb slightly or use a different choice of eigenfunctions.

## Appendix

### Eigenvalue Problem

We are solving:

$$
A x = \lambda x,
$$

where:

* $A \in \mathbb{R}^{n \times n}$ is a **square matrix** (input).
* $x \in \mathbb{R}^n$ is a **nonzero eigenvector** (output).
* $\lambda \in \mathbb{R}$ is the corresponding **eigenvalue** (output).

---

#### **Inputs**

* A square matrix $A$.

  * If symmetric: eigenvalues are real, eigenvectors are orthogonal.
  * If sparse: iterative methods are used.
  * If dense: direct factorization methods are used.

* Sometimes, a **generalized eigenproblem**:

  $$
  A x = \lambda B x,
  $$

  with $B$ symmetric positive definite (like the mass matrix in FEM/meshes).

  * Input: $A, B$.
  * Output: $\lambda, x$.

* Options for solver:

  * Number of eigenpairs to compute $k$.
  * Which part of the spectrum (smallest, largest, etc.).
  * Tolerance for convergence.

---

#### **Outputs**

* **Eigenvalues**: scalars $\lambda_1, \dots, \lambda_k$.
* **Eigenvectors**: corresponding vectors $x_1, \dots, x_k$.

They satisfy:

$$
A x_i = \lambda_i x_i
\quad \text{or} \quad
A x_i = \lambda_i B x_i.
$$

Normalization:

* Standard case: $ \|x_i\|_2 = 1$.
* Generalized case: $x_i^T B x_j = \delta_{ij}$.

---

#### **Methods**

* (a) Dense Methods (for small matrices)

  * **QR algorithm**: iteratively triangularizes $A$.
  * **Divide-and-conquer** or **Jacobi rotations**.
  * Cost: $O(n^3)$.

* (b) Sparse Methods (for large $n$)

  * **Power method**: finds largest eigenpair by repeated multiplication.
  * **Lanczos (ARPACK)**: builds a Krylov subspace, reduces to tridiagonal, solves small eigenproblem.
  * **LOBPCG**: block iterative method, good for generalized eigenproblems.

---

#### **Example**

Suppose:

$$
A =
\begin{bmatrix}
2 & 1 \\
1 & 2
\end{bmatrix}.
$$

***Step 1***: Solve $\det(A - \lambda I) = 0$.

$$
\det \begin{bmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{bmatrix}
= (2-\lambda)^2 - 1 = 0.
$$

$\lambda_1 = 1, \; \lambda_2 = 3$.

***Step 2***: Solve for $x$.

* For $\lambda_1 = 1$: $Ax = x \implies [2\;1;1\;2][x_1,x_2]^T = [x_1,x_2]^T$.
  ⇒ eigenvector $x = (1,-1)^T$.
* For $\lambda_2 = 3$: eigenvector $x = (1,1)^T$.

***Output***:

* Eigenvalues: $[1,3]$.
* Eigenvectors: $[(1,-1)^T, (1,1)^T]$.

---