---
title: What is Volume Meshing
permalink: /blogs/what-is-volume-meshing
medium: blog
category: what-is
---

## Overview

**Volume meshing** is the process of subdividing a **3D domain (a solid object or volume)** into smaller, simpler pieces called **elements**. These elements (tetrahedra, hexahedra, prisms, etc.) form a **volume mesh**, which is the foundation for numerical simulations in engineering and science.

In other words:

* You take a 3D shape (like a car engine block, a wing, or a human organ).
* You fill it with little 3D “bricks” (elements).
* Then, you run numerical methods (FEA, CFD, electromagnetics, etc.) on these bricks to approximate physics in the whole domain.

---

## Types

1. **Tetrahedra (4 nodes)** – flexible, automatic, good for complex shapes.
2. **Hexahedra (8 nodes)** – efficient, high accuracy, but harder to generate.
3. **Prisms/Wedges (6 nodes)** – useful for boundary layers in CFD.
4. **Pyramids/Polyhedra** – transition or general-purpose elements.

---

## Methods

1. **Surface Meshing**: Create a mesh of the object’s boundary (triangles or quads).
2. **Volume Filling**: Fill the inside with 3D elements using algorithms:
   * **Delaunay-based** (good quality, automatic)
   * **Advancing Front** (builds from surface inward)
   * **Octree/Grid-based** (fast, structured refinement)
3. **Refinement**: Adapt mesh to geometry and physics (smaller near corners, boundaries, or gradients).

---

## Applications

* **Structural FEA**: Stresses, deformations, crash simulations.
* **CFD**: Fluid flow, aerodynamics, heat transfer.
* **Electromagnetics**: Fields inside devices.
* **Medical imaging**: Blood flow in arteries, biomechanics.

---

## Considerations

* **Geometry complexity**: Tets/polyhedral for complex shapes; hex for simple, sweepable shapes.
* **Simulation type**: Hex preferred for structural; poly/hex/tet mix for CFD.
* **Boundary layer resolution**: Use prism/wedge elements near walls.
* **Solver compatibility**: Some solvers handle polyhedral or hybrid meshes better than others.
* **Mesh quality metrics**: Skewness, aspect ratio, and Jacobian determinant should be monitored.

---

## Libraries

Here are some of the most widely used open-source libraries for volume meshing, especially for **tetrahedral and hybrid meshes** in FEA/CFD/geometry processing.

---

* **General-Purpose Volume Mesh Generators**

  - **TetGen**

    * **Language:** C++ (with wrappers in Python, MATLAB)
    * **Strengths:**

      * Specialized in **Delaunay and constrained Delaunay tetrahedralization**
      * High-quality tetrahedral meshes
      * Handles surface meshes, holes, and constraints
    * **Use cases:** FEA preprocessing, biomedical modeling, geometry from CAD
    * [https://wias-berlin.de/software/tetgen](https://wias-berlin.de/software/tetgen)

  ---

  - **Gmsh**

    * **Language:** C++ with Python API
    * **Strengths:**

      * All-in-one: CAD modeling, surface meshing, **tetra/hex/prism volume meshing**
      * Supports Delaunay, Advancing Front, and transfinite (structured) meshing
      * Excellent for multi-physics simulations
    * **Use cases:** FEA/CFD pipeline, quick mesh generation with GUI or scripts
    * [http://gmsh.info](http://gmsh.info)

  ---

  - **Netgen**

    * **Language:** C++ with Python bindings
    * **Strengths:**

      * High-quality tetrahedral meshing (advancing front + Delaunay)
      * Used as meshing backend in NGSolve and some CAD software
    * **Use cases:** FEM workflows, structural and electromagnetic simulations
    * [https://ngsolve.org](https://ngsolve.org)

  ---

* **Geometry / Computational Libraries (with Meshing Modules)**

  - **CGAL (Computational Geometry Algorithms Library)**

    * **Language:** C++ (with limited Python wrappers)
    * **Strengths:**

      * State-of-the-art **3D Delaunay meshing algorithms**
      * Offers isotropic and adaptive refinement
      * Very robust for constrained Delaunay meshing
    * **Use cases:** Research, geometry processing, custom meshing workflows
    * [https://www.cgal.org](https://www.cgal.org)

  ---

  - **PyMesh**

    * **Language:** Python (C++ backend)
    * **Strengths:**

      * Wrapper around multiple meshing libraries (TetGen, CGAL, etc.)
      * Unified interface for mesh generation and processing
    * **Use cases:** Python workflows for geometry + volume meshing
    * [https://pymesh.readthedocs.io](https://pymesh.readthedocs.io)

  ---

  - **OpenCascade (with SMESH module)**

    * **Language:** C++ with Python bindings (via FreeCAD)
    * **Strengths:**

      * Industrial CAD kernel with meshing capabilities
      * Hexa/tetra/prism meshing options (SMESH)
    * **Use cases:** CAD + meshing integration (e.g., FreeCAD FEM workbench)
    * [https://www.opencascade.com](https://www.opencascade.com)

  ---

* **Domain-Specific Frameworks**

  - **OpenFOAM (snappyHexMesh)**

    * **Language:** C++
    * **Strengths:**

      * Primarily CFD mesher → **hex-dominant meshes with boundary layers**
      * Can generate hybrid meshes (hex, prism, tet)
    * **Use cases:** CFD simulations with complex geometries
    * [https://openfoam.org](https://openfoam.org)

  ---

  - **MFEM + GLVis (by LLNL)**

    * **Language:** C++ with Python interface
    * **Strengths:**

      * Finite element discretization library with mesh generation tools
      * Supports tetrahedral, hexahedral, and high-order meshes
    * **Use cases:** HPC and adaptive FEM workflows
    * [https://mfem.org](https://mfem.org)

  ---

* **Recommendation by Use Case**

  * **General FEA/CFD meshing (easy to use):** Gmsh, Netgen
  * **High-quality tetrahedral meshing (research/robust):** TetGen, CGAL
  * **Python workflows:** PyMesh, Gmsh (Python API)
  * **CAD + meshing integration:** OpenCascade (SMESH), FreeCAD FEM
  * **CFD-focused hex-dominant meshes:** OpenFOAM (snappyHexMesh)

---
