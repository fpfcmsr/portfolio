---
title: "FEMAP Labs"
date: 2026-11-04
draft: false
summary: "A portfolio of FEMAP/Nastran FEA, spanning static and dynamic analyses, joint modeling."
tags: ["FEMAP", "Nastran", "Finite Elements"]
---

## Overview

FEMAP/Nastran labs completed for Advanced Finite Element methods course, covering the full progression from 1D bar and truss elements through 2D and 3D solid stress analysis, nonlinear and buckling problems, and dynamic responses.

## Labs

![Lab 2: FEMAP interface](image2.png)

Lab 2: FEMAP interface showing the model tree, toolbars, and the active session window.

![Lab 3: 1D bar meshing](image3.png)

A straight bar converted to 1D elements with node and element labeling.

![Lab 4: Static FEA of a 1D rod](image4.png)

Boundary conditions and load applied to a meshed rod, with the Nastran input deck.

![Lab 5: Planar truss by orphan mesh](image5.png)

A planar truss built from manually placed 1D elements with an applied load.

![Lab 6: Planar truss by geometry](image6.png)

A truss generated from geometry with rod/beam properties assigned directly.

![Lab 7: Displacement-loaded 1D rod](image7.png)

A 1D rod with prescribed (displacement-controlled) boundary conditions.

![Lab 8: 3D truss in FEMAP/Nastran](image8.png)

A 3D space truss with its deformed shape and displacement results.

![Lab 9: Static FEA of a 2D beam](image9.png)

A meshed beam with an applied load and its deformed shape.

![Lab 10: 2D plane stress by orphan elements](image10.png)

A plate meshed with orphan 2D elements and a stress contour.

![Lab 11: 2D plane stress by geometry](image11.png)

A meshed plate with a von Mises stress distribution.

![Lab 12: Static FEA of a 2D wedge](image12.png)

A 3D wedge element model under load.

![Lab 13: 3D axisymmetric bodies](image13.png)

An axisymmetric mesh of a body of revolution.

![Lab 14: FEA of a 3D bracket](image14.png)

A bracket meshed with solid elements and a stress contour.

![Lab 15: Nonlinear FEA of a tapered tension member](image15.png)

A tapered bar under tension with its force–displacement curve.

![Lab 16: Linear buckling of a C-clamp](image16.png)

A C-clamp meshed for a linear buckling analysis with critical load factors.

![Lab 17: Bracket with a circular hole](image17.png)

Stress concentration around the hole in a loaded bracket.

![Lab 18: FEA of a pressure tank](image18.png)

A pressurized tank with a stress contour.

![Lab 19: Free vibration of a cantilever beam](image19.png)

Natural mode shapes of a cantilever beam.

![Lab 20: Static FEA of a C-clamp](image20.png)

Stress distribution in a C-clamp under a static load.

![Lab 21: Transient dynamic FEA of a UAV](image21.png)

A UAV wing structure with its transient dynamic response.

![Lab 22: RBE2s on assemblages of rods](image22.png)

RBE2 rigid links connecting rod nodes in an assemblage.

## Summary

These 21 labs walk through the complete FEMAP/Nastran workflow, ordered by increasing complexity. They begin with 1D elements — bar, truss (orphan mesh and geometry), and displacement-loaded rod — then move to beams and 2D plane-stress plates and wedge bodies, and on to 3D solids like a bracket, an axisymmetric member, and a pressurized tank. Later labs cover advanced behavior: nonlinear response, linear buckling, free vibration, and transient dynamics, and finish with joint modeling using RBE2 rigid links. Together they exercise meshing, load and constraint application, result recovery, and verification across static, nonlinear, buckling, and dynamic Nastran solvers.
