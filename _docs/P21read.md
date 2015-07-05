---
layout: docs
permalink: /docs/p21read/
title: P21read
---

**p21read** refers to one of many executables built from STEPcode. Each
p21read executable is specific to one EXPRESS schema and has a suffix indicating the schema. For example,

`p21read_sdai_IFC4
p21read_sdai_ISO15926
p21read_sdai_ap203
p21read_sdai_ap242`

p21read is useful for testing STEPcode. When invoked, it reads a Part 21 file into memory, creating an object to represent each instance. It then uses those objects methods to writes the instances to a new file. Warnings indicate potential problems, while errors indicate definite problems. Errors could be from one of three sources:

-   STEPcode itself
-   the Part 21 file
-   the EXPRESS schema

### Code

P21read can be found in the repo at [src/test/p21read/p21read.cc](https://github.com/stepcode/stepcode/blob/master/src/test/p21read/p21read.cc)

### Documentation

[Doxygen](http://stepcode.org/stepcode-use-doxygen/p21read_8cc.html)
