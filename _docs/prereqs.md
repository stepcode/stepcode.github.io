---
layout: docs
title: Prerequisites
permalink: /docs/prereqs/
---

Download STEPcode
-----------------

### Install git

Windows users: [msysgit](http://code.google.com/p/msysgit/) is known to
work. The app referenced in GitHub Bootcamp (link below) should work as
well.

For OSX, see [GitHub
Bootcamp](https://help.github.com/articles/set-up-git)

For Linux, install git through your package manager.

Alternately (not recommended): download an archive of the latest code
with **no** revision history by clicking
[here](https://github.com/stepcode/stepcode/zipball/master).

### Install CMake

Linux users, install cmake via your package manager. For OSX and
Windows, download from
[cmake.org](http://cmake.org/cmake/resources/software.html)

### Lexer and parser?

v0.7 and later **do not use** flex or bison. Generated lexer/parser code is included. If changes to that code are necessary, you will need [Baffled Citrus](https://github.com/stepcode/baffledcitrus) - perplex, lemon, and re2c.

### Clone the repository

From the command prompt:
`git clone git://github.com/stepcode/stepcode.git` Git will create a
directory *stepcode* and clone the repository there. Once done, the
latest revision will be checked out. You will be able to view revision
logs, switch branches, etc - see [Git
Basics](http://git-scm.com/book/en/Getting-Started-Git-Basics)
