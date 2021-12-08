---
title: "Xyz"
date: 2021-12-08T13:19:32+01:00

---

Open Cascade documentation: [gp_XYZ](https://dev.opencascade.org/doc/refman/html/classgp___x_y_z.html)

For example, [examples/ex04_xyz.nim]():

```nim
import occt

var xyz1 = newXyz(1.0, 0.2, 2.3)
echo "XYZ1: ", xyz1                          # XYZ1: Xyz(x:1.0, y:0.2000000029802322, z:2.299999952316284)
echo "Modulus: ", xyz1.modulus               # Modulus: 2.515949010848999
echo "SquareModulus: ", xyz1.squareModulus   # SquareModulus: 6.329999923706055

var xyz2 = newXyz(3.0, 1.0, -1.0)
echo "XYZ2: ", xyz2               # XYZ2: Xyz(x:3.0, y:1.0, z:-1.0)
xyz1.add(xyz2)                    
echo "XYZ1: ", xyz1               # XYZ1: Xyz(x:4.0, y:1.200000047683716, z:1.299999952316284)
xyz1 += xyz2
echo "XYZ1: ", xyz1               # XYZ1: Xyz(x:7.0, y:2.200000047683716, z:0.2999999523162842)

xyz1 = newXyz(1, 0,  0)           
xyz2 = newXyz(0, 1,  0)
xyz1.cross(xyz2)
echo xyz1                         # Xyz(x:0.0, y:0.0, z:1.0)
echo "SUM: ", xyz1, " + ", xyz2, " = ", xyz1 + xyz2   # SUM: Xyz(x:0.0, y:0.0, z:1.0) + Xyz(x:0.0, y:1.0, z:0.0) = Xyz(x:0.0, y:1.0, z:1.0)
```