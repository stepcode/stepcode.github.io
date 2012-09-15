---
title: Getting started
---

Download STEPcode
-----------------

### Install git

Windows users: use [msysgit](http://code.google.com/p/msysgit/), which
also includes working versions of bison and flex. The app referenced in
GitHub Bootcamp (link below) may work as well, but it does not include
bison and flex.

For OSX, see [GitHub
Bootcamp](https://help.github.com/articles/set-up-git)

For Linux, install git through your package manager.

Alternately (not recommended): download an archive of the current code
with **no** revision history by clicking
[here](https://github.com/stepcode/stepcode/zipball/master).

### Install CMake

Linux users, install cmake via your package manager. For OSX and
Windows, download from
[cmake.org](http://cmake.org/cmake/resources/software.html)

### Install Flex and Bison

Windows: If you did not install msysgit above, you will need
[bison](http://gnuwin32.sourceforge.net/packages/bison.htm) and
[flex](http://gnuwin32.sourceforge.net/packages/flex.htm). **Not all
versions work.** OSX and Linux: Flex and Bison were probably installed
with your compiler.

### Clone the repository

From the command prompt:

`git clone `[`git://github.com/stepcode/stepcode.git`](git://github.com/stepcode/stepcode.git)

Git will create a directory *stepcode* and clone the repository there.
Once done, the latest revision will be checked out. You will be able to
view revision logs, switch branches, etc - see [Git
Basics](http://git-scm.com/book/en/Getting-Started-Git-Basics)

Build STEPcode
--------------

See **[Building STEPcode](Building STEPcode "wikilink")**. STEPcode uses
CMake, which is cross-platform and somewhat different from the
traditional unix './configure && make'

Use STEPcode
------------

See **[How to use STEPcode in an
application](How to use STEPcode in an application "wikilink")**

Exploring STEPcode
------------------

[Description of the files and
directories](Files and directories "wikilink")
