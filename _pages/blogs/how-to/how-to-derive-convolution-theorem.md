---
title: How to Derive Convolution Theorem
permalink: /blogs/how-to-derive-convolution-theorem
medium: blog
category: how-to
tags: 
  - ai
---

## Step 1: Representing Convolution as Matrix Multiplication

The first key insight is that **convolution with a fixed filter can be represented as multiplication by a circulant matrix.**

Let $ \mathbf{h} = [h_0, h_1, ..., h_{N-1}]^T $ be our filter kernel. The convolution of $ \mathbf{h} $ with a signal $ \mathbf{x} = [x_0, x_1, ..., x_{N-1}]^T $, assuming cyclic (circular) convolution, is given by:
$$
\mathbf{y} = \mathbf{h} * \mathbf{x}
$$
where $ y_n = \sum_{m=0}^{N-1} h_{(n-m) \mod N}  x_m $.

This linear operation can be written as:
$$
\mathbf{y} = C_{\mathbf{h}} \mathbf{x}
$$
where $ C_{\mathbf{h}} $ is the **circulant matrix** formed from $ \mathbf{h} $:
$$
C_{\mathbf{h}} = \begin{bmatrix}
h_0 & h_{N-1} & h_{N-2} & \cdots & h_1 \\
h_1 & h_0 & h_{N-1} & \cdots & h_2 \\
h_2 & h_1 & h_0 & \cdots & h_3 \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
h_{N-1} & h_{N-2} & h_{N-3} & \cdots & h_0
\end{bmatrix}
$$

Notice that each row is a cyclic shift of the previous row. The first row is $ \mathbf{h}^T $, the second row is $ S \mathbf{h} $ (where $ S $ is the shift operator), the third is $ S^2 \mathbf{h} $, and so on.

## Step 2: The Circulant Matrix is a Polynomial of the Shift Operator

The fundamental shift operator $ S $ is diagonalized by the DFT matrix $ F $:

$$
S = F \Lambda_S F^{-1}
$$

where $ \Lambda_S $ is a diagonal matrix containing the eigenvalues of $ S $, which are the DFT of its first row $[0, 1, 0, ..., 0]$.

- If a matrix $ A $ is diagonalizable as $ A = F \Lambda F^{-1} $, then any polynomial of $ A $ is also diagonalized by the same $ F $:
    $$
    p(A) = F  p(\Lambda)  F^{-1}
    $$
    where $ p(\Lambda) $ is the same polynomial applied to the diagonal matrix (which is trivial, as it just applies $ p(\cdot) $ to each diagonal element).

Applying this to our circulant matrix $ C_{\mathbf{h}} $, which is a polynomial $ p(S) $:

$$
C_{\mathbf{h}} = h_0 I + h_1 S + h_2 S^2 + ... + h_{N-1} S^{N-1} = F (h_0 I + h_1 \Lambda_S + h_2 \Lambda_S^2 + ... + h_{N-1} \Lambda_S^{N-1}) F^{-1}
$$

Let's denote the diagonal matrix in the middle as $ \Lambda_{\mathbf{h}} $:
$$
\Lambda_{\mathbf{h}} = h_0 I + h_1 \Lambda_S + h_2 \Lambda_S^2 + ... + h_{N-1} \Lambda_S^{N-1}
$$

Therefore, the diagonalization of the circulant matrix is:
$$
C_{\mathbf{h}} = F \Lambda_{\mathbf{h}} F^{-1}
$$

## Step 3: Identifying the Diagonal Matrix $ \Lambda_{\mathbf{h}} $

What are the entries of $ \Lambda_{\mathbf{h}} $? Since it's a diagonal matrix, let's look at its $ k $-th diagonal element.

- The $ k $-th diagonal element of $ \Lambda_S $ is the $ k $-th eigenvalue of $ S $, which we found to be $ \omega_N^{-k} = e^{-2\pi i k / N} $.
- The $ k $-th diagonal element of $ \Lambda_S^m $ is therefore $ (\omega_N^{-k})^m = \omega_N^{-k m} $.
- Thus, the $ k $-th diagonal element of $ \Lambda_{\mathbf{h}} $ is:
    $$
    (\Lambda_{\mathbf{h}})_{kk} = h_0 + h_1 \omega_N^{-k} + h_2 \omega_N^{-2k} + ... + h_{N-1} \omega_N^{-(N-1)k}
    $$

But this is precisely the formula for the $ k $-th coefficient of the **DFT of $ \mathbf{h} $**!

$$
(\Lambda_{\mathbf{h}})_{kk} = \hat{h}_k = \text{DFT}(\mathbf{h})_k
$$

So, the diagonal matrix $ \Lambda_{\mathbf{h}} $ is simply $ \text{diag}(\hat{\mathbf{h}}) $, a diagonal matrix whose entries are the DFT coefficients of the filter $ \mathbf{h} $.

$$
C_{\mathbf{h}} = F \cdot \text{diag}(\hat{\mathbf{h}}) \cdot F^{-1}
$$

## Step 4: Deriving the Convolution Theorem

We are now ready to prove the Convolution Theorem. We start with convolution in the spatial domain:
$$
\mathbf{y} = C_{\mathbf{h}} \mathbf{x} = \mathbf{h} * \mathbf{x}
$$

Substitute the diagonalized form of $ C_{\mathbf{h}} $:
$$
\mathbf{y} = F \cdot \text{diag}(\hat{\mathbf{h}}) \cdot F^{-1} \mathbf{x}
$$

Now, let's interpret this equation in the frequency domain. Recall:

- $ F^{-1} \mathbf{x} = \hat{\mathbf{x}} $ is the DFT of the input signal.
- $ F^{-1} \mathbf{y} = \hat{\mathbf{y}} $ is the DFT of the output signal.

To get $ \hat{\mathbf{y}} $, we apply $ F^{-1} $ to both sides of the equation:
$$
F^{-1} \mathbf{y} = F^{-1} ( F \cdot \text{diag}(\hat{\mathbf{h}}) \cdot F^{-1} \mathbf{x} )
$$
$$
\hat{\mathbf{y}} = (F^{-1} F) \cdot \text{diag}(\hat{\mathbf{h}}) \cdot \hat{\mathbf{x}}
$$
$$
\hat{\mathbf{y}} = I \cdot \text{diag}(\hat{\mathbf{h}}) \cdot \hat{\mathbf{x}}
$$

Since $ \text{diag}(\hat{\mathbf{h}}) \cdot \hat{\mathbf{x}} $ is a diagonal matrix multiplying a vector, it is equivalent to an **element-wise multiplication** (Hadamard product) of the vectors $ \hat{\mathbf{h}} $ and $ \hat{\mathbf{x}} $:

$$
\hat{\mathbf{y}} = \hat{\mathbf{h}} \odot \hat{\mathbf{x}}
$$

Or, component-wise:
$$
\hat{y}_k = \hat{h}_k \cdot \hat{x}_k \quad \text{for } k = 0, 1, ..., N-1
$$

## The Convolution Theorem

This final result is the Convolution Theorem:

> **Circular convolution in the spatial/time domain is equivalent to element-wise multiplication in the frequency domain.**

$$
\boxed{\mathbf{h} * \mathbf{x} \quad \xrightarrow{\mathcal{F}} \quad \hat{\mathbf{h}} \odot \hat{\mathbf{x}}}
$$

Where $ \mathcal{F} $ denotes the Discrete Fourier Transform.
