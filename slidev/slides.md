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
  * **GEOMETRY** original CAD modeler 
  * **SHAPER** a **freecad** like CAD modeler
* Meshing: **MESH** with plugins **MeshGems**, **Gmsh**, **Netgen**, ..
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

* From [Salome website](https://www.salome-platform.org/?page_id=2433), select the archive tarball for your os:

```bash
tar zxvf SALOME-....tgz -C /opt/
mv /opt/SALOME-9.13.0-native-DB12-SRC /opt/SALOME-9.13.0-native
cd /opt/SALOME-9.13.0-native
./install_bin.sh
sat config SALOME-9.13.0-native --check_system
salome test
/opt/SALOME/salome 
```

* Docker

```bash
xhost +local:root
docker run [-runtime=nvidia --gpus all -e NVIDIA_DRIVER_CAPABILITIES=all] -it --rm  --name salome -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix trophime/salome:9.13.0-bookworm
```

* Singularity
```bash
singularity pull salome-9.13.sif
```

💡 Salome is already installed on Unistra PC 💡
   `/opt/SALOME-9.13.0-native-DB12-SRC/salome`


---
layout: two-cols
---
# **Geometry** module

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
hideInToc: true
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
transition: fade-out
layout: two-cols
level: 3
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module

* 📷 Camera

  | **Operation** | Mouse | Trackpad |
  | --------- | ----- | -------- |
  | Zoom  | ctrl left click |  ctrl left click |  
  | Rotation  | ctrl right click |  ctrl right click |  
  | Translation  | ctrl Wheel |  ctrl multi-finger |


::right::

![](/img/salome-modules.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube

::right::

![](/img/salome-cube.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder

::right::

![](/img/salome-cube-cyl.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"
* Create Groups
* Save CAD as XAO

::right::

![](/img/salome-movecyl.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"

::right::

![](/img/salome-cube-w-cyl.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"

::right::

![](/img/salome-whatis.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"
* Create Groups

::right::

![](/img/salome-extract.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"
* Create Groups

::right::

![](/img/salome-groupface.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"
* Create Groups
* Save CAD as XAO

::right::

![](/img/salome-exportXAO.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"
* Create Groups
* Save CAD as XAO
* Dump python script

::right::

![](/img/salome-dump.png)
---
transition: fade-out
layout: two-cols
level: 3
hideInToc
---

# Cube with hole (GUI mode)

* Start salome:

```bash
salome [-w1] [-m GEOM,SMESH]
```

* Select **Geometry** module
* Create Cube and Cylinder
* Move the Cylinder
* Perform the "cut"
* Create Groups
* Save CAD as XAO

::right::

![](/img/salome-savestudy.png)

---
layout: two-cols
level: 3
---

# Cube with hole (TUI mode)

```python
import salome
salome.salome_init()
 
from salome.geom import geomBuilder
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
```

To run:
```bash
./[mesa_]salome [-t] cube-trou.py
```

```bash
./run_salome.bat [-t] cube-trou.py
```
::right::
<img src="/img/salome-TUI-cube.png" />


---
hideInToc: true
level: 3
---

# Cube with hole (TUI mode)

* add params

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--dx", type=float, help="set dx length")
...
args = parser.parse_args()

Box_1 = geompy.MakeBoxDXDYDZ(args.dx, args.dy, args.dz)
Cylinder_1 = geompy.MakeCylinderRH(args.R, args.H)
geompy.TranslateDXDYDZ(Cylinder_1, args.dx/2., args.dy/2., -args.dz/4.)
Cut_1 = geompy.MakeCutList(Box_1, [Cylinder_1], True)
```

To run:

```bash
./[mesa_]salome [-t] test.py args:--dx=2,--dy=2,..
```
```bash
./run_salome.bat [-t] test.py args:--dx=2,--dy=2,..
```

::right::

---
level: 3
hideInToc: true
---

# Cube with hole (TUI mode)

* Get id for Boundaries
  
<img src="/img/salome-getface.png" />

---
level: 3
hideInToc: true
---

# Cube with hole (TUI mode)

* Get id for Boundaries
  

```python
T = geompy.MakeVertex(0, 0, args.dz)
Top = geompy.GetShapesOnPlaneWithLocation(Cut_1, geompy.ShapeType["FACE"], OZ, T, GEOM.ST_ON)
GTop = geompy.CreateGroup(Cut_1, geompy.ShapeType["FACE"])
geompy.UnionList(GTop, Top)
geompy.addToStudyInFather(Cut_1, GTop, "GTop")

Hole_Faces = geompy.GetShapesOnShape(Cylinder_1, Cut_1, geompy.ShapeType["FACE"], GEOM.ST_ONIN)

HoleBord = geompy.CreateGroup(Cut_1, geompy.ShapeType["FACE"])
faces_ids = [geompy.GetSubShapeID(Cut_1, sub_face) for sub_face in Hole_Faces]
geompy.UnionIDs(HoleBord, faces_ids)

Bord = geompy.CreateGroup(Cut_1, geompy.ShapeType["FACE"])
Faces = geompy.ExtractShapes(Cut_1, geompy.ShapeType["FACE"]) 
geompy.UnionList(Bord, Faces)
geompy.DifferenceList(Bord, Hole_Faces)
```


---
layout: two-cols
level: 3
hideInToc: true
---

# Cube with hole (TUI mode)

* Save CAD:
  * see [methods](https://docs.salome-platform.org/latest/gui/GEOM/geompy_doc/group__l2__import__export.html)
  * Use **XAO** format
    * [`ExportXAO()`](https://docs.salome-platform.org/latest/gui/GEOM/geompy_doc/group__l2__import__export.html#ga05cf9a41b29418ea475d43bf7b6d4eaa)
    * Format: xml: for groups + brep
    * Split into 2 files: xml + brep

```python
ExportXao(Cut_1, [Bord,Holes], None, "author", "Cut_1.xao", "Cut_1.brep")
```

💡Load in gmsh: since 4.13 💡

```bash
gmsh Cut_1.xao
```

::right::

  
---
layout: two-cols
level: 3
hideInToc: true
---

# Boolean Operations


| [Gmsh](https://gmsh.info/doc/texinfo/gmsh.html#Boolean-operations)     | [Salome](https://docs.salome-platform.org/latest/gui/GEOM/geompy_doc/group__l3__boolean.html#ga844f6f2affb6d492c56cba33ab959b81)                                                    |
| --------------------------------------- | ----------------------------------------------------------- |
| <code>BooleanIntersection</code>        | <code>MakeCommon</code>                                 |
| <code>BooleanUnion</code>               | <code>MakeFuse</code>                                  |
| <code>BooleanDifference</code>          | <code>MakeCut</code>         |
| <code>BooleanFragments</code>           | <code>MakePartition</code>                                   |


---
layout: two-cols
level: 3
hideInToc: true
---


# Load CAD geometry

* see [Import methods](https://docs.salome-platform.org/latest/gui/GEOM/geompy_doc/group__l2__import__export.html)

```python
Object = ImportXao("Cut_1.xao")
```

⚠️ may fails because of the path to the step file ⚠️

```xml
<shape format="BREP" file="/data/geometries/Oxford9-Axi.brep"/>
```


# Defeaturing

* 😟 only in **SHAPER**

---
layout: two-cols
---

# **Mesh** Module

* Structured Mesh
* Unstructed Mesh

---
layout: two-cols
level: 2
---

# Structured Mesh
---
layout: two-cols
level: 2
---

# UnStructured Mesh (TUI)

* **Netgen** plugin

```python
from salome.smesh import smeshBuilder
smesh = smeshBuilder.New()

Mesh_1 = smesh.Mesh(Cut_1)
NETGEN_ = Mesh_1.Tetrahedron(algo=smeshBuilder.NETGEN_1D2D3D)
NETGEN_3D_Params = NETGEN_.Parameters(smeshBuilder.SIMPLE)
NETGEN_3D_Params.SetNumberOfSegments( 15 )
…

isDone = Mesh_1.Compute()
```

---
layout: two-cols
level: 2
hideInToc: true
---

# UnStructured Mesh (TUI)

* **MeshGems** plugin (requires a valid license)

```python
from salome.smesh import smeshBuilder
smesh =  smeshBuilder.New()

# create a mesh on the box
mgtetraMesh = smesh.Mesh(box,"box: MG-Tetra and MG-CADSurf mesh")

# create a MG_CADSurf algorithm for faces
MG_CADSurf = mgtetraMesh.Triangle(algo=smeshBuilder.MG_CADSurf)
MG_Tetra = mgtetraMesh.Tetrahedron(algo=smeshBuilder.MG_Tetra)

# compute the mesh
mgtetraMesh.Compute()
```

---
layout: two-cols
level: 2
hideInToc: true
---

# UnStructured Mesh (TUI)

* Create Groups from geometry

```python
import SMESH

Cut_1_1 = Mesh_1.GroupOnGeom(Cut_1,'Cut_1',SMESH.VOLUME)
Group_1_1 = Mesh_1.GroupOnGeom(Group_1,'Group_1',SMESH.FACE)
[ Box_1_1, Face_1_1, Face_2_1, Face_3_1, Face_4_1, Face_5_1, Face_6_1 ] = Mesh_1.GetGroups()

## Set names of Mesh objects
smesh.SetName(Box_1_1, 'Cut_1')
```

* Save Mesh with MED Format

```python
Mesh_1.ExportMED( r'testcube.med', 0, SMESH.MED_V2_2, 1, None ,1)
```

* Convert to msh format

```bash
gmsh -0 testcube.med -o testcube.msh
```

  
---
layout: two-cols
level: 3
hideInToc: true
---

# Quad Mesh

* **Hexablock** plugin
* **Hexotic** plugin (requires a valid licence)

---
layout: two-cols
level: 2
---

# Adapt Mesh

---
layout: two-cols
level: 2
---

# Moving Mesh

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://docs.salome-platform.org/latest/main/index.html) · [Github](https://github.com/SalomePlatform) · [Tutorials](https://www.youtube.com/channel/UCokrSqnpG3sLXkagZwUmuXg)

<PoweredBySlidev mt-10 />
