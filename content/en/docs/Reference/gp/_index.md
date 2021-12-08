---
title: "Package: gp"
date: 2021-12-08T11:57:15+01:00

---

Open Cascade documentation: [gp](https://dev.opencascade.org/doc/refman/html/package_gp.html).

This package provides the following:

- [Pnt](pnt): defines a 3D cartesian point.
- [Xyz](xyz): describes a cartesian coordinate entity in 3D space {X,Y,Z}. This entity is used for algebraic calculation. This entity can be transformed with a "Trsf" or a "GTrsf" from package "gp". It is used in vectorial computations or for holding this type of information in data structures.
- [Vec](vec): defines a non-persistent vector in 3D space.


- gp_Ax2
- gp_Ax22d
- gp_Ax2d
- gp_Ax3
- gp_Circ
- gp_Circ2d
- gp_Cone
- gp_Cylinder
- gp_Dir
- gp_Dir2d
- gp_Elips
- gp_Elips2d
- gp_EulerSequence
- gp_GTrsf
- gp_GTrsf2d
- gp_Hypr
- gp_Hypr2d
- gp_Lin
- gp_Lin2d
- gp_Mat
- gp_Mat2d
- gp_Parab
- gp_Parab2d
- gp_Pln
- gp_Pnt2d
- gp_Quaternion
- gp_QuaternionNLerp
- gp_QuaternionSLerp
- gp_Sphere
- gp_Torus

- gp_Trsf
- gp_Trsf2d
- gp_TrsfForm
- gp_TrsfNLerp

- gp_Vec2d
- gp_Vec2f
- gp_Vec3f
- gp_VectorWithNullMagnitude
- gp_XY


Some "sugar" is added for this package:

1. You can mix floats and integers while defining the points.
2. You can assign values like `pnt.x = 8` and get the value with: `echo pnt.x`
3. The same applies with: `pnt[0] = 8`  and `echo pnt[0]`

