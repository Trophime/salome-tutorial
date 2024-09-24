---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Salome Tutorial
info: |
  ## Slidev Starter Template
  a guide to start with Salome.
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Welcome to Salome Tutorial

Presentation slides for Salome beginners

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
layout: two-cols
---

# What is Salome?


An opensource platform for simulation.

Provides modules for:
* CAD: 
  * **GEOMETRY**
  * **SHAPER**
* Meshing: **MESH** with plugins **MeshGems**, **Gmsh**,..
* PostProcessing: **PARAVIS**

Other modules include:

* Solver:
* Advanced tools:
* Workflow

::right::
<img src="/img/salome-BARCOM.png" />

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
hideInToc: true
---

# Table of contents

<Toc v-click minDepth="1" maxDepth="2"></Toc>

---


# Installation

* From [Salome website](https://www.salome-platform.org/?page_id=2433), select get tarball archive for your os:

  ```bash
  tar zxvf -C /opt/SALOME ..
  cd /opt/SALOME
  ./install_bin.sh
  sat config SALOME-${VERSION}-native --check_system
  salome test
  /opt/SALOME/salome 
  ```

* Container
  * Docker

  ```bash
  xhost +local:root
  docker run [-runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all] -it --rm  --name salome -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix trophime/salome:9.13.0-bookworm
  ```

  * Singularity
  ```bash
  singularity pull salome-9.13.sif
  ```

For this tutorial, we recommend to use the archive tarball from salome.


---
layout: two-cols
---
# Salome Geometry module

* GUI mode
  * Select a module
  * Dump commands to a python script
  * Save 'Study' in hdf5 format

* TUI mode
  * Replay python script
  * Batch mode

::right::

<iframe width="480" height="240" src="https://www.youtube.com/embed/srL10n7j2eQ?list=PLgvBxFyGVRbZZz4wVvP36xXQL-S81RZsc" title="SALOME Geometry Module" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---
layout: two-cols
level: 2
---

# Workflow

* Create base objects
* Perform boolean operations
* Get id for geom entities
* Save to CAD format
* Dump a python Script

::right::

<!-- youtube: srL10n7j2eQ -->

---
layout: two-cols
level: 3
---

# Cube with hole (GUI mode)



---
layout: two-cols
level: 3
---

# Cube with hole (TUI mode)

```python
from salome.geom import geomBuilder
import math
import SALOMEDS

geompy = geomBuilder.New()

O = geompy.MakeVertex(0, 0, 0)
OZ = geompy.MakeVectorDXDYDZ(0, 0, 1)

Box_1 = geompy.MakeBoxDXDYDZ(200, 200, 200)
Cylinder_1 = geompy.MakeCylinder(O, OZ, 80, 300)
geompy.TranslateDXDYDZ(Cylinder_1, 100, 100, -50)
Cut_1 = geompy.MakeCutList(Box_1, [Cylinder_1], True)

geompy.addToStudy( Box_1, 'Box_1' )
geompy.addToStudy( Cylinder_1, 'Cylinder_1' )
geompy.addToStudy( Cut_1, 'Cut_1' )

if salome.sg.hasDesktop():
  salome.sg.updateObjBrowser()
```

::right::

---
layout: two-cols
hideInToc: true
level: 3
---

# Cube with hole

* add params

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--dx", type=float, help="set dx length")

Box_1 = geompy.MakeBoxDXDYDZ(args.dx, args.dy, args.dz)
Cylinder_1 = geompy.MakeCylinderRH(args.R, args.H)
geompy.TranslateDXDYDZ(Cylinder_1, args.dx/2., args.dy/2., -args.dz/4.)
Cut_1 = geompy.MakeCutList(Box_1, [Cylinder_1], True)
```

::right::

---
layout: two-cols
hideInToc: true
level: 3
---

# Cube with hole

* add params

On Linux:
```bash
./[mesa_]salome [-t] test.py args:--dx=2,--dy=2,..
```

On Windows:
```bash
./run_salome.bat ….
```

::right::

---
layout: two-cols
level: 3
hideInToc: true
---

# Cube with hole

* Get id for Boundaries
* Save CAD as XAO file
  * Split into 2 files: xml + brep
  
```python
import GEOM
import sys
import salome

…
Box_1 = geompy.MakeBoxDXDYDZ(args.dx, args.dy, args.dz)
Cylinder_1 = geompy.MakeCylinderRH(args.R, args.H)
geompy.TranslateDXDYDZ(Cylinder_1, args.dx/2., args.dy/2., -args.dz/4.)
Cut_1 = geompy.MakeCutList(Box_1, [Cylinder_1], True)

T = geompy.MakeVertex(0, 0, args.dz)
Top = geompy.GetShapesOnPlaneWithLocation(Cut_1, geompy.ShapeType["FACE"], OZ, T, GEOM.ST_ON)
GTop = geompy.CreateGroup(Cut_1, geompy.ShapeType["FACE"])
geompy.UnionList(GTop, Top)
geompy.addToStudyInFather(Cut_1, GTop, "GTop")

Hole_Faces = geompy.GetShapesOnShape(Cylinder_1, Cut_1, geompy.ShapeType["FACE"], GEOM.ST_ONIN)
print(f"Len(faces)={len(Hole_Faces)}”)
HoleBord = geompy.CreateGroup(Cut_1, geompy.ShapeType["FACE"])
faces_ids = [geompy.GetSubShapeID(Cut_1, sub_face) for sub_face in Hole_Faces]
geompy.UnionIDs(HoleBord, faces_ids)
Bord = geompy.CreateGroup(Cut_1, geompy.ShapeType["FACE"])
Faces = geompy.ExtractShapes(Cut_1, geompy.ShapeType["FACE"]) 
geompy.UnionList(Bord, Faces)
geompy.DifferenceList(Bord, Hole_Faces)
```

::right::

---
layout: two-cols
level: 3
hideInToc: true
---

# Boolean Operations

---
layout: two-cols
level: 3
hideInToc: true
---

# Load CAD geometry



---
layout: two-cols
---

# Meshing

* Structured Mesh
* Unstructed Mesh

---
layout: two-cols
level: 2
hideInToc: true
---

# Structured Mesh
---
layout: two-cols
level: 2
hideInToc: true
---

# UnStructured Mesh
---
layout: two-cols
level: 2
hideInToc: true
---

# Quad Mesh

---
layout: two-cols
---

# Adapt Mesh

---
layout: two-cols
---
# Moving Mesh

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://docs.salome-platform.org/latest/main/index.html) · [Github](https://github.com/SalomePlatform) · [Tutorials](https://www.youtube.com/channel/UCokrSqnpG3sLXkagZwUmuXg)

<PoweredBySlidev mt-10 />
