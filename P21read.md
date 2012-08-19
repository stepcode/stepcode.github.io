---
title: P21read
---

**p21read** refers to one of many executables built from STEPcode. Each
p21read executable is specific to one EXPRESS schema.

This executable is useful for testing STEPcode; it reads a Part 21 file
into memory and writes it to a new file. Any errors indicate problems,
but not the source.

Errors could be from one of three sources:

-   STEPcode itself
-   the Part 21 file
-   the EXPRESS schema

### Source

P21read can be foud in the repo on GitHub at
[src/test/p21read/p21read.cc](https://github.com/stepcode/stepcode/blob/master/src/test/p21read/p21read.cc)

### Documentation

[Doxygen](http://stepcode.org/stepcode-use-doxygen/p21read_8cc.html)
