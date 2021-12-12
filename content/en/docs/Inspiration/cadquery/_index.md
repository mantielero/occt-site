---
title: "Cadquery"
date: 2021-12-12T11:00:50+01:00
---

# Workplanes
Workplanes are defined within [cq.py](https://github.com/CadQuery/cadquery/blob/84edaf5d76eb1968137a2337e1008539838cd0e3/cadquery/cq.py#L134). An explanation of the concept is given [here](https://cadquery.readthedocs.io/en/latest/primer.html?highlight=workplane#workplane-class).

Workplanes have a center and a coordenate system.

In Nim we could do with:
```nim
type
  Workplane = object
    cs:Ax2  # Coordinate system
```

In cadquery, the Workplane contains:
- `objects: List[CQObject]`
- `ctx: CQContext`
- `parent: Optional["Workplane"]`
- `plane: Plane`
- `_tag: Optional[str]`

In the workplane, we work in 2d. CadQuery support [this 2d operations](https://cadquery.readthedocs.io/en/latest/apireference.html#doperations). 


