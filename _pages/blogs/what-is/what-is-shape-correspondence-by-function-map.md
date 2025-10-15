---
title: What is Shape Correspondence by Function Map
permalink: /blogs/what-is-shape-correspondence-by-function-map
medium: blog
category: what-is
tags:
  - geometry
---

## The Core Idea: Eigenfunctions as a Universal Basis

In modern shape analysis the **Laplace-Beltrami Operator (LBO)** is fundamental for constructing a canonical, geometry-aware function space on a manifold (a 3D shape).

Think of the standard Fourier analysis on a flat, 1D line. We decompose a complex signal into a sum of simple sine and cosine waves, which are the eigenfunctions of the second derivative operator ($ \frac{d^2}{dx^2} $). The different frequencies (eigenvalues) form a natural basis.

The Laplace-Beltrami operator ($ \Delta $) is the generalization of the second derivative to functions defined on curved surfaces. Its eigenfunctions form a natural, **geometry-aware basis** for the space of functions defined on that surface.

Let's formalize the eigenproblem:

$$
\Delta \phi_i = \lambda_i \phi_i
$$

where:
* $ \lambda_i $ is the $ i $-th eigenvalue (a scalar, often sorted so that $ \lambda_1 \leq \lambda_2 \leq \lambda_3 \leq ... $).
* $ \phi_i $ is the corresponding $ i $-th eigenfunction.

The set of these eigenfunctions $ \{ \phi_1, \phi_2, \phi_3, ... \} $ is what we use to construct our function space.

---

## Why is this Powerful for Shape Correspondence?

This LBO-based function space is the foundation for many correspondence algorithms. Here’s how it's used:

### 1. Functional Maps
This is the most direct application. The Functional Maps framework posits that if two shapes $ S $ and $ T $ are similar, a correspondence between them induces a linear mapping between their LBO-based function spaces.

If $ f $ is a function on $ S $ and $ g $ is the corresponding function on $ T $, the map $ T_F $ that sends $ f $ to $ g $ is called a **functional map**. Crucially, in the LBO basis $ \{\phi_i^S\} $ and $ \{\phi_i^T\} $, this linear map $ T_F $ can be represented as a small **matrix $ C $**.

Finding correspondence reduces to finding the matrix $ C $ that satisfies certain constraints (e.g., preserving known corresponding functions). This is a much simpler and more robust problem than finding point-to-point maps directly.

### 2. Global Point Signatures (GPS) and Heat Kernel Signatures (HKS)
These are powerful **point descriptors** derived from the LBO basis.

*   **GPS:** For a point $ p $, its GPS is the vector $ (\frac{\phi_1(p)}{\sqrt{\lambda_1}}, \frac{\phi_2(p)}{\sqrt{\lambda_2}}, ... ) $. This provides a canonical, isometry-invariant "coordinate" for each point.
*   **HKS:** Defined as $ HKS(p, t) = \sum_{i=1}^{\infty} e^{-\lambda_i t} \phi_i(p)^2 $. It describes the amount of heat remaining at point $ p $ after time $ t $, and is also intrinsic.

**For Correspondence:** You can compute these descriptors for every point on two shapes. Corresponding points will have similar descriptor vectors. This provides powerful constraints for matching.

### 3. ShapeDNA / Spectral Embeddings
The sequence of eigenvalues $ \{\lambda_i\} $ itself is a shape descriptor, often called the "ShapeDNA." It is invariant to rotation, translation, and isometry. Furthermore, embedding a shape into a spectral space by using the first $ k $ eigenfunctions as coordinates ($ p \rightarrow (\phi_1(p), \phi_2(p), ..., \phi_k(p)) $) can be used for segmentation and correspondence.

---

## Step-by-Step Process for Construction

### Step 1: Discretize the Shape and the LBO

In practice, we work with discrete shapes (triangle meshes). The continuous surface is represented by a set of vertices $ V $ and triangles $ F $. We must also discretize the LBO itself.

The most common discretization is the **cotangent weight scheme**, which leads to a generalized eigenvalue problem:

$$
\mathbf{A}^{-1} \mathbf{L} \mathbf{\phi}_i = \lambda_i \mathbf{\phi}_i
$$

where:
* $ \mathbf{L} $ is the **stiffness matrix** (cotangent Laplacian), a sparse matrix where entry $ L_{ij} $ is based on the cotangents of the angles opposite to the edge between vertices $ i $ and $j$.
* $ \mathbf{A} $ is the **mass matrix**, which accounts for the local area around each vertex. It's often a diagonal matrix (lumped mass matrix) for efficiency.
* $ \mathbf{\phi}_i $ is now a vector of values at each vertex, representing the discrete eigenfunction.

### Step 2: Solve the Eigenproblem

We solve the generalized eigenvalue problem:

$$
\mathbf{L} \mathbf{\phi}_i = \lambda_i \mathbf{A} \mathbf{\phi}_i
$$

We compute the first $ k $ smallest eigenvalues and their corresponding eigenvectors. In practice, $ k $ can be a few hundred. These eigenvectors are the discrete analogs of the continuous eigenfunctions.

**Key Properties of this Basis:**
1.  **Orthogonality:** The eigenvectors are orthogonal with respect to the mass matrix:

$$ 
\langle \mathbf{\phi}_i, \mathbf{\phi}_j \rangle_A = \mathbf{\phi}_i^T \mathbf{A} \mathbf{\phi}_j = 0 \text{ ( for } i \neq j \text{ )}
$$

2.  **Completeness:** The set of all eigenfunctions forms a complete basis. This means any square-integrable function on the shape can be represented as a linear combination of them.
3.  **Intrinsic Geometry:** The basis is purely derived from the shape's intrinsic geometry (distances on the surface), not its extrinsic embedding (how it sits in 3D space). This makes it invariant to isometries (bending).

### Step 3: The Functional Map Matrix $ \mathbf{C} $

Any function $ f $ on $ \mathcal{M} $ can be represented in the LBO basis:

$$
f = \sum_{i=1}^k a_i \phi_i^\mathcal{M} = \mathbf{\Phi}^\mathcal{M} \mathbf{a}
$$

where $ \mathbf{a} = (a_1, ..., a_k)^T $ are the spectral coefficients.

The functional map $ T_F $ sends $ f $ to a function $ g = T_F(f) $ on $ \mathcal{N} $, which has its own representation:

$$
g = \sum_{j=1}^k b_j \phi_j^\mathcal{N} = \mathbf{\Phi}^\mathcal{N} \mathbf{b}
$$

The magic: **The map between coefficients $ \mathbf{a} \to \mathbf{b} $ is linear** and can be represented by a matrix $ \mathbf{C} $:

$$
\mathbf{b} = \mathbf{C} \mathbf{a}
$$

Thus, $ \mathbf{C} $ is a $ k \times k $ matrix that defines the functional map.

### Step 4: Computing $ \mathbf{C} $ from Corresponding Functions

We need known corresponding functions between the shapes to constrain $ \mathbf{C} $. Common choices:

#### **Option A: Descriptor Preservation**

Use point-wise descriptors that should be preserved by the correspondence:

* **Heat Kernel Signatures (HKS):** $ HKS(p, t) = \sum_{i=1}^k e^{-\lambda_i t} (\phi_i(p))^2 $

For each descriptor function $ f $ on $ \mathcal{M} $ and its corresponding $ g $ on $ \mathcal{N} $, we get a constraint:

1. Project the functions onto the LBO bases:

   $$
   \mathbf{a} = (\mathbf{\Phi}^\mathcal{M})^T \mathbf{A}^\mathcal{M} \mathbf{f}
   $$

   $$
   \mathbf{b} = (\mathbf{\Phi}^\mathcal{N})^T \mathbf{A}^\mathcal{N} \mathbf{g}
   $$

2. The constraint becomes: $ \mathbf{b} = \mathbf{C} \mathbf{a} $

If we have $ m $ pairs of corresponding functions, we can stack them:

$$
\mathbf{B} = \mathbf{C} \mathbf{A}
$$

where $ \mathbf{A} = [\mathbf{a}_1 \| \mathbf{a}_2 \| \cdots \| \mathbf{a}_m] $ and $ \mathbf{B} = [\mathbf{b}_1 \| \mathbf{b}_2 \| \cdots \| \mathbf{b}_m] $.

We solve for $ \mathbf{C} $ using least squares:

$$
\mathbf{C} = \mathbf{B} \mathbf{A}^+ \quad \text{(where } \mathbf{A}^+ \text{ is pseudoinverse)}
$$

#### **Option B: Known Point Correspondences**

If we have some known point-to-point matches $ p_i \in \mathcal{M} \leftrightarrow q_i \in \mathcal{N} $, we can create corresponding indicator functions or use the constraint that the functional map should preserve the correspondence:

The key equation: for corresponding points $ p \leftrightarrow q $, we want:

$$
\sum_j C_{ij} \phi_j^\mathcal{M}(p) \approx \phi_i^\mathcal{N}(q) \quad \forall i
$$

In matrix form for all correspondences:

$$
\mathbf{\Phi}^\mathcal{N}_\text{corr} = \mathbf{C} \cdot \mathbf{\Phi}^\mathcal{M}_\text{corr}
$$

where $ \mathbf{\Phi}^\mathcal{M}_\text{corr} $ contains the eigenvectors evaluated at the corresponding points on $ \mathcal{M} $.

### Step 5: Converting Functional Map to Point-to-Point Correspondence

Once we have $ \mathbf{C} $, we can recover a point-to-point map:

For each point $ p $ on $ \mathcal{M} $:

* Compute its spectral coordinate: $ \mathbf{a}_p = (\phi_1^\mathcal{M}(p), ..., \phi_k^\mathcal{M}(p)) $
* Map to target shape: $ \mathbf{b}_p = \mathbf{C} \mathbf{a}_p $
* Find nearest neighbor on $ \mathcal{N} $ in spectral space:

  $$
  T(p) = \arg\min_{q \in \mathcal{N}} \|\mathbf{\Phi}^\mathcal{N}(q) - \mathbf{b}_p\|
  $$

  where $ \mathbf{\Phi}^\mathcal{N}(q) = (\phi_1^\mathcal{N}(q), ..., \phi_k^\mathcal{N}(q)) $

---

## Appendix

### Laplace-Beltrami Operator

#### **1. Continuous Definition on a Smooth Manifold**

On a smooth Riemannian manifold $ \mathcal{M} $, the Laplace-Beltrami operator $ \Delta $ is a generalization of the standard Laplacian ($ \nabla^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2} + \frac{\partial^2}{\partial z^2} $) to curved surfaces.

It is defined intrinsically, meaning it only depends on the metric tensor $ g $ of the manifold (i.e., distances on the surface), not on how it is embedded in space.

**General Formula (Coordinate-Invariant):**
For a function $ f: \mathcal{M} \rightarrow \mathbb{R} $, the LBO is defined as the divergence of the gradient:

$$
\Delta f = \text{div}(\nabla f)
$$

where:
* $ \nabla f $ is the **gradient** of $ f $, a vector field pointing in the direction of the greatest increase of $ f $ on the manifold.
* $ \text{div} $ is the **divergence**, which measures the magnitude of a source or sink at a given point in a vector field.

---

#### **2. Discrete Formulation on a Triangle Mesh**

In practice, a 3D shape is represented as a triangle mesh $ M = (V, E, F) $, where:

* $ V = \{\mathbf{v}_1, \mathbf{v}_2, ..., \mathbf{v}_n\} $ is the set of vertices.
* $ E $ is the set of edges.
* $ F $ is the set of triangular faces.

A function $ f $ on the mesh is defined by its values at the vertices: $ f = (f_1, f_2, ..., f_n)^T $, where $ f_i = f(\mathbf{v}_i) $.

The goal is to find a discrete operator $ \mathbf{L} $ (a matrix) such that $ \mathbf{L} \mathbf{f} $ approximates the continuous $ \Delta f $.

**2.1 The Cotangent Weight Scheme (The Standard Discretization)**

This is the most common and geometrically accurate discretization. The key idea is to compute the LBO at a vertex $ \mathbf{v}_i $ by integrating over its neighboring triangles.

The formula for the component $ (\Delta f)_i $ at vertex $ \mathbf{v}_i $ is:

$$
(\Delta f)_i = \frac{1}{A_i} \sum_{j \in \mathcal{N}(i)} (\cot \alpha_{ij} + \cot \beta_{ij}) (f_j - f_i)
$$

Let's break this down:

* $ \mathcal{N}(i) $: The set of vertices connected to $ \mathbf{v}_i $ by an edge (the one-ring neighborhood).
* $ \alpha_{ij}, \beta_{ij} $: The two angles opposite to the edge $ (i, j) $.
* $ A_i $: The **Voronoi area** of vertex $ \mathbf{v}_i $.
* $ f_j, f_i $: The function values at vertices $ \mathbf{v}_j $ and $ \mathbf{v}_i $.

**2.2. Constructing the System Matrices**

The discrete LBO is represented as a matrix system. We have two key matrices:

**2.2.1. The Stiffness Matrix (Cotangent Laplacian), $ \mathbf{L} $**

This is a symmetric $ n \times n $ matrix that contains the cotangent weights. Its entries are defined as:

$$
L_{ij} =
\begin{cases}
-\frac{1}{2} \sum_{k \in \mathcal{N}(i)} (\cot \alpha_{ik} + \cot \beta_{ik}) & \text{if } i = j \\
\frac{1}{2} (\cot \alpha_{ij} + \cot \beta_{ij}) & \text{if } (i, j) \text{ is an edge} \\
0 & \text{otherwise}
\end{cases}
$$

**Important Note:** The off-diagonal term $ \frac{1}{2} $ comes from the fact that the cotangent weight for an edge is shared between the two stiffness matrices of its endpoints when assembling the global system. Some sources absorb this factor into the definition, so you might see it without the $ \frac{1}{2} $. The version above is common in finite element literature.

**2.2.2. The Mass Matrix, $ \mathbf{A} $**

This is a diagonal $ n \times n $ matrix that encodes the local area around each vertex. The most accurate choice is the **Voronoi area** (or "lumped mass matrix").

The Voronoi area $ A_i $ for a vertex $ \mathbf{v}_i $ is calculated by summing contributions from all its adjacent triangles. For a triangle $ T $ adjacent to $ \mathbf{v}_i $, if all angles are acute, the contribution is the area of the Voronoi cell around $ \mathbf{v}_i $ within $ T $, which is:

$$
\frac{1}{8} \sum_{j \in \mathcal{N}(i)} (\cot \alpha_{ij} + \cot \beta_{ij}) \|\mathbf{v}_j - \mathbf{v}_i\|^2 
$$

A more robust formula that handles obtuse triangles is:

$$
A_i = \frac{1}{3} \sum_{T \in \mathcal{N}(i)} \text{Area}(T)
$$

This is the **barycentric mass matrix**, where the vertex gets one-third of the area of every adjacent triangle. It is less accurate but more stable and is very commonly used.

Thus, the mass matrix is:

$$
A_{ij} =
\begin{cases}
A_i & \text{if } i = j \\
0 & \text{otherwise}
\end{cases}
$$

**2.2.3. The Final Discrete Laplace-Beltrami Operator**

With these matrices, the action of the discrete LBO on a function vector $ \mathbf{f} $ is given by:

$$
\Delta \mathbf{f} \approx \mathbf{A}^{-1} \mathbf{L} \mathbf{f}
$$

This means to get the value of $ \Delta f $ at all vertices, you compute $ \mathbf{L} \mathbf{f} $ and then scale each row by the inverse of the vertex's area.

---

### Function Projection

#### **1. Continuous Case**

Recall that the LBO eigenfunctions form an **orthonormal basis** with respect to the inner product induced by the area element:

$$
\langle \phi_i, \phi_j \rangle = \int_{\mathcal{M}} \phi_i(x) \phi_j(x) \, dA(x) = \delta_{ij}
$$

where $ \delta_{ij} $ is the Kronecker delta (1 if $ i = j $, 0 otherwise).

This means any square-integrable function $ f $ on the manifold can be expanded as:

$$
f(x) = \sum_{i=1}^\infty a_i \phi_i(x)
$$

where the coefficients $ a_i $ are obtained by **projection**:

$$
a_i = \langle f, \phi_i \rangle = \int_{\mathcal{M}} f(x) \phi_i(x) \, dA(x)
$$

#### **2. Discrete Case Derivation**

Now, let's see how this translates to discrete triangle meshes.

**2.1. Discrete Inner Product**

The continuous inner product $ \langle f, g \rangle = \int_{\mathcal{M}} f(x) g(x) \, dA(x) $ becomes a weighted sum over vertices in the discrete setting:

$$
\langle f, g \rangle \approx \mathbf{f}^T \mathbf{A} \mathbf{g} = \sum_{i=1}^n A_{ii} f_i g_i
$$

where $ \mathbf{A} $ is the mass matrix (diagonal in the simplest case), and $ A_{ii} $ represents the area element around vertex $ i $.

**Why the mass matrix?** Because we're numerically integrating the product $ f(x)g(x) $ over the surface. For a piecewise-linear function on a triangle mesh, the appropriate quadrature gives us this mass matrix formulation.

**2.2. Discrete Orthogonality**

The discrete eigenfunctions satisfy:

$$
(\mathbf{\phi}_i)^T \mathbf{A} \mathbf{\phi}_j = \delta_{ij}
$$

This is the discrete analog of $ \int_{\mathcal{M}} \phi_i \phi_j dA = \delta_{ij} $.

**2.3. Projection Formula Derivation**

We want to represent a function $ \mathbf{f} $ (an $ n \times 1 $ vector) in the LBO basis:

$$
\mathbf{f} = \sum_{i=1}^k a_i \mathbf{\phi}_i = \mathbf{\Phi} \mathbf{a}
$$

where $ \mathbf{\Phi} = [\mathbf{\phi}_1 \| \mathbf{\phi}_2 \| \cdots \| \mathbf{\phi}_k] $ is an $ n \times k $ matrix.

To find the coefficients $ a_i $, we use the orthogonality. Take the inner product of both sides with $ \mathbf{\phi}_j $:

$$
\langle \mathbf{f}, \mathbf{\phi}_j \rangle = \langle \sum_{i=1}^k a_i \mathbf{\phi}_i, \mathbf{\phi}_j \rangle
$$

Using linearity of the inner product:

$$
\langle \mathbf{f}, \mathbf{\phi}_j \rangle = \sum_{i=1}^k a_i \langle \mathbf{\phi}_i, \mathbf{\phi}_j \rangle
$$

But due to orthogonality, $ \langle \mathbf{\phi}_i, \mathbf{\phi}_j \rangle = \delta_{ij} $, so:

$$
\langle \mathbf{f}, \mathbf{\phi}_j \rangle = \sum_{i=1}^k a_i \delta_{ij} = a_j
$$

Therefore:

$$
a_j = \langle \mathbf{f}, \mathbf{\phi}_j \rangle = \mathbf{f}^T \mathbf{A} \mathbf{\phi}_j
$$

In matrix form for all coefficients:

$$
\mathbf{a} = \mathbf{\Phi}^T \mathbf{A} \mathbf{f}
$$
