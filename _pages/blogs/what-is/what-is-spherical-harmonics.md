---
title: What is Spherical Harmonics
permalink: /blogs/what-is-spherical-harmonics
medium: blog
category: what-is
tags:
  - geometry
---

## What are Spherical Harmonics?

**Spherical harmonics** are special mathematical functions defined on the surface of a sphere. Think of them as the spherical equivalent of the sine and cosine waves in Fourier analysis, but adapted to spherical geometry.

Just as any sound wave can be broken down into combinations of pure sine waves, **any function on a sphere can be expressed as a sum of spherical harmonics**. They form a complete basis for functions defined on the sphere's surface.

## Derivation

### The Starting Point: Laplace's Equation in Spherical Coordinates

We begin with Laplace's equation in three dimensions:

$$
\nabla^2 V = 0
$$

This equation describes potentials in regions with no mass/charge (like gravity outside a planet or electrostatics outside a charged sphere). In spherical coordinates $(r, \theta, \phi)$, the Laplacian operator $\nabla^2$ takes the following form:

$$
\nabla^2 V = \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 \frac{\partial V}{\partial r} \right) + \frac{1}{r^2 \sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial V}{\partial \theta} \right) + \frac{1}{r^2 \sin^2 \theta} \frac{\partial^2 V}{\partial \phi^2} = 0
$$

Our goal is to find functions $V(r, \theta, \phi)$ that satisfy this equation.

### Step 1: Separation of Variables

The key insight is to assume that the solution can be written as a product of functions, each depending on only one coordinate:

$$
V(r, \theta, \phi) = R(r) \cdot \Theta(\theta) \cdot \Phi(\phi)
$$

We now substitute this product back into Laplace's equation. The derivatives become:

- $\frac{\partial V}{\partial r} = \Theta \Phi \frac{dR}{dr}$
- $\frac{\partial V}{\partial \theta} = R \Phi \frac{d\Theta}{d\theta}$
- $\frac{\partial^2 V}{\partial \phi^2} = R \Theta \frac{d^2\Phi}{d\phi^2}$

Plugging these in:

$$
\Theta \Phi \cdot \frac{1}{r^2} \frac{d}{dr} \left( r^2 \frac{dR}{dr} \right) + R \Phi \cdot \frac{1}{r^2 \sin \theta} \frac{d}{d\theta} \left( \sin \theta \frac{d\Theta}{d\theta} \right) + R \Theta \cdot \frac{1}{r^2 \sin^2 \theta} \frac{d^2\Phi}{d\phi^2} = 0
$$

To clean this up, we multiply the entire equation by $ \frac{r^2}{R \Theta \Phi} $ (assuming our functions are not zero):

$$
\underbrace{\frac{1}{R} \frac{d}{dr} \left( r^2 \frac{dR}{dr} \right)}_{\text{Function of } r} + \underbrace{\frac{1}{\Theta \sin \theta} \frac{d}{d\theta} \left( \sin \theta \frac{d\Theta}{d\theta} \right) + \frac{1}{\Phi \sin^2 \theta} \frac{d^2\Phi}{d\phi^2}}_{\text{Function of } \theta \text{ and } \phi} = 0
$$

This equation has a powerful consequence. The first term depends only on $r$, while the second group of terms depends only on $\theta$ and $\phi$. For their sum to be zero for *all* values of $r, \theta, \phi$, each part must be equal to a constant. We call this constant $\lambda$, leading to two separate equations:

1. **The Radial Equation:**

    $$
    \frac{d}{dr} \left( r^2 \frac{dR}{dr} \right) = \lambda R
    $$
    (We won't focus on solving this here, as it's not part of the angular solution).

2. **The Angular Equation:**

    $$
    \frac{1}{\Theta \sin \theta} \frac{d}{d\theta} \left( \sin \theta \frac{d\Theta}{d\theta} \right) + \frac{1}{\Phi \sin^2 \theta} \frac{d^2\Phi}{d\phi^2} + \lambda = 0
    $$

### Step 2: Separating the Angular Part

We now apply separation of variables *again* to the angular equation. Let $Y(\theta, \phi) = \Theta(\theta)\Phi(\phi)$. Multiply the angular equation by $\sin^2 \theta$:

$$
\frac{\sin \theta}{\Theta} \frac{d}{d\theta} \left( \sin \theta \frac{d\Theta}{d\theta} \right) + \lambda \sin^2 \theta + \frac{1}{\Phi} \frac{d^2\Phi}{d\phi^2} = 0
$$

Now, the first two terms depend only on $\theta$, and the last term depends only on $\phi$. Again, for their sum to be zero for all angles, each part must be equal to a constant. By convention, we call this constant $-m^2$.

This gives us two final, ordinary differential equations:

**A. The Azimuthal Equation (in $\phi$):**

$$
\frac{d^2\Phi}{d\phi^2} = -m^2 \Phi
$$

This is the classic simple harmonic oscillator equation. Its solutions are complex exponentials (or sines and cosines):

$$
\Phi(\phi) = e^{im\phi}
$$

For the function to be single-valued on the sphere (i.e., $\Phi(\phi + 2\pi) = \Phi(\phi)$), $m$ must be an integer: $m = 0, \pm 1, \pm 2, \dots$

**B. The Polar Equation (in $\theta$):**

We are left with the equation for $\Theta(\theta)$. Substituting the constant $-m^2$ gives:

$$
\frac{1}{\sin \theta} \frac{d}{d\theta} \left( \sin \theta \frac{d\Theta}{d\theta} \right) + \left( \lambda - \frac{m^2}{\sin^2 \theta} \right) \Theta = 0
$$

### Step 3: Solving the Polar Equation - The Associated Legendre Equation

To solve the polar equation, it's standard to make a change of variable: let $x = \cos\theta$. Consequently, $\sin^2 \theta = 1 - x^2$ and the derivative transforms as $\frac{d}{d\theta} = -\sin\theta \frac{d}{dx}$.

After some algebra (applying the chain rule), the polar equation transforms into the **Associated Legendre Equation**:

$$
\frac{d}{dx} \left[ (1 - x^2) \frac{d\Theta}{dx} \right] + \left[ \lambda - \frac{m^2}{1-x^2} \right] \Theta = 0
$$

For the special case $m=0$, this reduces to the standard **Legendre's Differential Equation**:

$$
\frac{d}{dx} \left[ (1 - x^2) \frac{dP}{dx} \right] + \lambda P = 0
$$

The solutions to Legendre's equation are the **Legendre Polynomials**, $P_l(x)$, which are finite polynomials. For these solutions to be non-singular and physically admissible on the interval $[-1, 1]$ (which corresponds to $\theta$ from $0$ to $\pi$), the separation constant $\lambda$ must take the form:

$$
\lambda = l(l+1) \quad \text{where } l = 0, 1, 2, \dots
$$

The solutions for non-zero $m$ are the **Associated Legendre Functions**, denoted $P_l^m(x)$. They can be generated from the Legendre polynomials using the formula:

$$
P_l^m(x) = (-1)^m (1 - x^2)^{m/2} \frac{d^m}{dx^m} P_l(x)
$$

Again, for the solutions to be well-behaved, $m$ must be an integer bounded by $l$: $m = -l, -l+1, \dots, 0, \dots, l-1, l$.

### Step 4: Putting the Angular Parts Together

We have now found the two angular parts:

- From the polar equation: $\Theta(\theta) \propto P_l^m(\cos\theta)$
- From the azimuthal equation: $\Phi(\phi) \propto e^{im\phi}$

Therefore, the combined angular solution is:

$$
Y_l^m(\theta, \phi) \propto P_l^m(\cos\theta) e^{im\phi}
$$

The final step is **normalization**. We choose the constant of proportionality such that the functions are orthonormal over the surface of the sphere. The standard normalization gives us the final, precise definition:

$$
Y_l^m(\theta, \phi) = \sqrt{\frac{(2l+1)}{4\pi} \frac{(l-m)!}{(l+m)!}}  P_l^m(\cos\theta)  e^{im\phi}
$$

## Properties

### Orthonormality

The spherical harmonics form a complete orthonormal basis for square-integrable functions on the unit sphere $L^2(S^2)$:

$$
\int_{0}^{2\pi} \int_{0}^{\pi} Y_l^m(\theta,\phi) Y_{l'}^{m'*}(\theta,\phi) \sin\theta  d\theta  d\phi = \delta_{l l'} \delta_{m m'}
$$

Where:

- $\delta_{ij}$ is the Kronecker delta
- $*$ denotes complex conjugation
- $\sin\theta d\theta d\phi = d\Omega$ is the surface element on the sphere

**Vector Space Interpretation:** This means the spherical harmonics are like "unit vectors" in the infinite-dimensional space of functions on the sphere, and they're all mutually perpendicular.

### Completeness

Any square-integrable function $f(\theta,\phi)$ on the sphere can be expanded as:

$$
f(\theta,\phi) = \sum_{l=0}^{\infty} \sum_{m=-l}^{l} a_l^m Y_l^m(\theta,\phi)
$$

The expansion coefficients are given by the inner product:

$$
a_l^m = \langle f, Y_l^m \rangle = \int_{S^2} f(\theta,\phi) Y_l^{m*}(\theta,\phi)  d\Omega
$$

This is the spherical analogue of the Fourier series expansion.

### Complex Conjugation

$$
Y_l^{m*}(\theta,\phi) = (-1)^m Y_l^{-m}(\theta,\phi)
$$

This property is useful for working with real-valued functions and ensures that real combinations can be formed.

### Rotation Properties

Under a rotation $R$ of the coordinate system, spherical harmonics transform as:

$$
Y_l^m(R^{-1}\hat{\mathbf{n}}) = \sum_{m'=-l}^{l} D_{mm'}^{(l)}(R) Y_l^{m'}(\hat{\mathbf{n}})
$$

Where $D_{mm'}^{(l)}(R)$ are the Wigner D-matrices, which form a $(2l+1)$-dimensional representation of the rotation group SO(3).

The most common parameterization uses **Euler angles** $ (\alpha, \beta, \gamma) $:

$$
D^{(l)}_{mm'}(\alpha, \beta, \gamma) = e^{-im\alpha} d^{(l)}_{mm'}(\beta) e^{-im'\gamma}
$$

Where:

- $ \alpha \in [0, 2\pi] $: Rotation around z-axis
- $ \beta \in [0, \pi] $: Rotation around y-axis  
- $ \gamma \in [0, 2\pi] $: Rotation around z-axis again

The real-valued **Wigner small d-matrices** $ d^{(l)}_{mm'}(\beta) $ describe rotations around the y-axis:

$$
d^{(l)}_{mm'}(\beta) = \langle l, m | e^{-i\beta \hat{J}_y} | l, m' \rangle
$$

These have explicit formulas:

$$
d^{(l)}_{mm'}(\beta) = \sqrt{(l+m)!(l-m)!(l+m')!(l-m')!} \times \sum_k \frac{(-1)^{k+m-m'}}{k!(l+m-k)!(l-m'-k)!(k+m'-m)!} \left(\cos\frac{\beta}{2}\right)^{2l+m-m'-2k} \left(\sin\frac{\beta}{2}\right)^{2k+m'-m}
$$

The sum is over all integer $ k $ for which the factorials are non-negative.
