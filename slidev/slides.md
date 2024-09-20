---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Gmsh Tutorial
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
---

# What is Salome?


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

* From Salome website, select get tarball archive for your os:

```bash
untar
install
check
run 
```

* Container
  * Docker

```bash
docker pull trophime/salome:9.13
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
* TUI mode

::right::



---
layout: two-cols
level: 2
---

# Workflow

* Create base objects
* Perform boolean operations
* Get id for geom entities
* Save to CAD format

::right::

<!-- youtube: srL10n7j2eQ -->

---
layout: two-cols
level: 3
---

# Cube with hole


::right::

---
layout: two-cols
level: 3
hideInToc: true
---

# Cube with holes


::right::

```gmsh
...
```

# Load CAD geometry


---

# TUI mode


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
