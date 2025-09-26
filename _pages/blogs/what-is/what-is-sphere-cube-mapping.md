---
title: What is Sphere-Cube Mapping
permalink: /blogs/what-is-sphere-cube-mapping
medium: blog
category: what-is
tags: 
  - geometry
---

## Overview

A **cubemap** is a way of representing directions (or points on the sphere) using the **six faces of a cube**.

* Imagine a unit cube centered at the origin.
* Each direction vector $(x,y,z)$ from the origin intersects one of the six cube faces.
* That intersection is projected onto a 2D square (the cube face).
* The six squares together form the **cubemap texture**.

This is widely used for environment maps (skyboxes, reflections), but the same projection can be used for **sphere → cube surface parameterization**.

---

## Sphere → Cube

Given a point on the unit sphere $(x,y,z)$:

1. Find the dominant axis:

   $$
   a = \arg\max(|x|, |y|, |z|)
   $$

   → decides which cube face the point maps to (±X, ±Y, ±Z).

2. Project onto that cube face:

   * For example, if $a = x$ and $x > 0$ → use the **+X face**.
   * The 2D coordinates on that face are:

     $$
     u = \frac{y}{|x|}, \quad v = \frac{z}{|x|}
     $$
   * Similar formulas for the other five faces.

3. Normalize $u, v$ to $[0,1]$ for texture coordinates.

Thus every sphere point has a unique $(\text{face}, u,v)$ coordinate.

---

## Cube → Sphere

If you start with cube face coordinates:

* Given cube face (+X, -X, +Y, -Y, +Z, -Z) and normalized $(u,v)$,
* Convert back to 3D cube coordinates $(x,y,z)$,
* Normalize vector to unit length → gives point on sphere.

This is how environment maps are sampled.

---

## Distortions

* **Good:**

  * No singularities (unlike spherical coordinates with poles).
  * Distortion is more uniform than equirectangular projection.
  * Easy to implement.
* **Bad:**

  * Discontinuities along cube edges/corners.
  * Distortion is still anisotropic (stretching near edges).

---
