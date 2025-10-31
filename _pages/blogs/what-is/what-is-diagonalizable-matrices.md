---
title: What is Diagonalizable Matrices
permalink: /blogs/what-is-diagonalized-matrices
medium: blog
category: what-is
tags: 
  - ai
---

## Definition of Diagonalizable Matrices

A matrix is **diagonalizable** if it is *similar* to a diagonal matrix.

In simpler terms, you can transform it into a pure diagonal matrix by changing your perspective (your coordinate system).

An $n \times n$ matrix $A$ is **diagonalizable** if there exists an **invertible** matrix $P$ and a **diagonal** matrix $D$ such that:

$$
A = P D P^{-1}
$$

or, equivalently:

$$
D = P^{-1} A P
$$

Let's dissect this equation:

- $A$: The original, potentially complex, matrix.
- $D$: A **diagonal matrix**. This means all its entries are zero except for those on the main diagonal.
    $$
    D = \begin{bmatrix}
    \lambda_1 & 0 & \cdots & 0 \\
    0 & \lambda_2 & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots \\
    0 & 0 & \cdots & \lambda_n
    \end{bmatrix}
    $$
- $P$: The **change of basis** matrix (or the eigenvector matrix). Its columns are the **eigenvectors** of $A$.
- $P^{-1}$: The inverse of $P$. This transforms the coordinates back to the standard basis.

The operation $P^{-1} A P$ is called a **similarity transformation**. It's like looking at the same linear transformation from a different, much simpler point of view.

## The Power of Diagonalizable Matrices

- **Easy Matrix Powers:**

Computing $A^k$ (for large $k$) is very difficult for a general matrix. But if $A = P D P^{-1}$, then:

$$
A^k = (P D P^{-1})^k = P D (P^{-1}P) D (P^{-1}P) ... D P^{-1} = P D^k P^{-1}
$$

And since $D$ is diagonal, $D^k$ is trivial to compute: you just raise each diagonal element to the power $k$.

$$
D^k = \begin{bmatrix}
\lambda_1^k & 0 & \cdots & 0 \\
0 & \lambda_2^k & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & \lambda_n^k
\end{bmatrix}
$$

- **Understanding the Matrix's Action:**

The equation $A = P D P^{-1}$ gives us a clear recipe for what $A$ does to any vector $x$:

- Decompose $x$ into the eigenvectors (the columns of $P$). This is what $P^{-1}x$ does. It finds the "coordinates" of $x$ in the eigenvector basis.
- Scale each component independently by the corresponding eigenvalue. This is what $D$ does.
- Reassemble the scaled components back into the standard basis. This is what $P$ does.

So, instead of a complicated mixing operation, the matrix $A$ simply **scales** in the directions of its eigenvectors.

## Relation with Eigenvectors and Eigenvalues

The definition $A = P D P^{-1}$ is directly equivalent to the concept of eigenvectors and eigenvalues.

If you multiply both sides of $A = P D P^{-1}$ by $P$ on the right, you get:

$$
A P = P D
$$

Now, look at the columns of $P$. Let's call them $\mathbf{v}_1, \mathbf{v}_2, ..., \mathbf{v}_n$. Looking at the matrix multiplication column-by-column, the equation $A P = P D$ becomes:

$$
A \mathbf{v}_i = \lambda_i \mathbf{v}_i \quad \text{for } i = 1, 2, ..., n
$$

This is the **eigenvalue equation**! The columns of $P$ *must* be the eigenvectors of $A$, and the diagonal entries of $D$ ($\lambda_i$) *must* be the corresponding eigenvalues.

**Therefore, a matrix is diagonalizable if and only if it has a full set of $n$ linearly independent eigenvectors.**

## Definition of Jointly Diagonalizable Matrices

Two or more matrices are **jointly diagonalizable** if they can be diagonalized *using the same eigenvector basis* (the same change-of-basis matrix $P$).

A set of $n \times n$ matrices $A_1, A_2, ..., A_k$ is **jointly diagonalizable** if there exists a single **invertible** matrix $P$ and diagonal matrices $D_1, D_2, ..., D_k$ such that for every matrix in the set:

$$
A_i = P D_i P^{-1} \quad \text{for all } i = 1, 2, ..., k
$$

This can be equivalently written as:
$$
D_i = P^{-1} A_i P
$$

## The Power of Jointly Diagonalizable Matrices

- **They All Commute:**

  A fundamental theorem in linear algebra states that two matrices are jointly diagonalizable **if and only if** they **commute**.

  $$
  A_i A_j = A_j A_i \quad \text{for every pair } (i, j)
  $$

  This means the order in which you apply these transformations doesn't matter. This is a very strong property.

- **Operations are Simplified:**

  Any algebraic operation you perform on these matrices becomes incredibly simple in the shared diagonal basis.

  - **Sums:** $A + B = P D_A P^{-1} + P D_B P^{-1} = P (D_A + D_B) P^{-1}$. The sum is also diagonalized by $P$.
  - **Products:** $A B = (P D_A P^{-1})(P D_B P^{-1}) = P (D_A D_B) P^{-1}$. The product is also diagonalized by $P$, and since diagonal matrices commute, $D_A D_B = D_B D_A$, proving $AB = BA$.
  - **Polynomials:** Any polynomial function $f(A, B)$ can be computed by simply applying the function to the corresponding diagonal elements.
