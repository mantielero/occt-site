---
title: "Handles"
date: 2021-12-11T09:41:08+01:00

---

# Handles
This is smart pointers used by Open Cascade.

A detailed explanation on handles is given the Open Cascade documentation: [Programming with Handles](https://dev.opencascade.org/doc/overview/html/occt_user_guides__foundation_classes.html#occt_fcug_2_2).

They are just references to values. So different references can point to the same object. Once all the references come out of scope, the object is destroyed.


# Nim
## Basic example
The following code does the following:
```nim
import occt

var aPnt:HandleGeom_CartesianPoint

aPnt = newHandle( cnew newGeomCartesianPoint(1.1, 2.2, 3.3) )
echo `*`(aPnt).x
`*`(aPnt).setY(1.3)

echo `*`(aPnt).y
```

1. The code `var aPnt:HandleGeom_CartesianPoint` creates the variable `aPnt` with type `HandleGeom_CartesianPoint`. Bear in mind that `HandleGeom_CartesianPoint` is an alias for: `Handle[CartesianPoint]`.
2. The code `cnew newGeomCartesianPoint(0.0,0.0,0.0)` creates a `ptr Geom_CartesianPoint`. This can be automatically converted to `HandleGeom_CartesianPoint` thanks to a converter defined in `standard_handle.nim`.
3. The code `aPnt = newHandle( cnew newGeomCartesianPoint(0.0,0.0,0.0) )` creates a `HandleGeom_CartesianPoint` from the `ptr Geom_CartesianPoint`.
4. The code:
   ```nim
   echo `*`(aPnt).x
   ```
   is used to show the content of `aPnt` through the handle. For that purpose, we use the operator `*` which converts `HandleGeom_CartesianPoint` into `var Geom_CartesianPoint`.
5. The code:
   ```nim
   *`(aPnt).setY(1.3)`
   ```
   is used for assigment by means of the handle.

In the above example, memory is handled by C++ side part of the history.

## One to many example
The following example shows how two handles point to the same object:
```nim
import occt

# Create the pointer to the object
var aPntPtr = cnew newGeomCartesianPoint(1.1, 2.2, 3.3) 

# Create handles for the object
var aPntHandle1, aPntHandle2: HandleGeom_CartesianPoint
aPntHandle1 = newHandle( aPntPtr )
aPntHandle2 = newHandle( aPntPtr )

# We can now access to the same object through different handles
assert `*`(aPntHandle1).x == `*`(aPntHandle2).x 
assert `*`(aPntHandle1).y == `*`(aPntHandle2).y
assert `*`(aPntHandle1).z == `*`(aPntHandle2).z

# If we modify something using one handle, the other can see it.
`*`(aPntHandle1).setY(1.3)
assert `*`(aPntHandle1).y == `*`(aPntHandle2).y
echo `*`(aPntHandle1).y

echo "All assertions were true!!"
```

## Wayforward
With a couple of function is very easy to simplify the coding. The first one, creates a constructor for handles. The second one is a converter that enables using the handle as if it were the object itself:
```nim
import occt

proc newPointCartesian[X,Y,Z:SomeNumber](x:X; y:Y, z:Z):HandleGeom_CartesianPoint =
  newHandle( cnew newGeomCartesianPoint(x.cfloat, y.cfloat, z.cfloat) )

converter toGeom_CartesianPoint*(tmp:HandleGeom_CartesianPoint):var Geom_CartesianPoint  =
  `*`(tmp)

# Create the pointer to the object
var aPnt2:HandleGeom_CartesianPoint
var aPnt1 = newPointCartesian(1, 2.2, 3.3)
echo aPnt1.x, " ", aPnt1.y, " ", aPnt1.z
echo "aPnt is null: ", aPnt1.isNull, " ", aPnt2.isNull

aPnt2 = aPnt1
echo aPnt2.y
echo aPnt1.y

aPnt1.setY(5.5)
echo aPnt2.y
echo aPnt1.y
```

# Future ideas:
## Type conformity
https://dev.opencascade.org/doc/overview/html/occt_user_guides__foundation_classes.html#autotoc_md64

This can be implemented by means of something like:
```
converter toGeom_Point*(tmp:HandleGeom_CartesianPoint):HandleGeom_Point  {.importcpp:"(@)", header:"Geom_Point.hxx",cdecl.}
```

So that the following works:
```nim
var aPnt1:HandleGeom_Point
var aPnt2:HandleGeom_CartesianPoint
aPnt2 = newPointCartesian(1, 2.2, 3.3)
aPnt1 = aPnt2  # This creates automatic conversion thanks to C++ side type conformity (it would be wrong in Nim). Thanks to the converter.
```

# Proposal
1. The type used in Nim could be directly the handle.
2. Needs to be defined how to work with inheritance:

   - Option 1: inheritance between handles.
   - Option 2: using types as a mean to simulate inheritance.
