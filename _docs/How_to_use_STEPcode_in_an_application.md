---
layout: docs
permalink: /docs/usage2/
title: How to use STEPcode in an application
---

## CMake Integration

-   Use **SC_IS_SUBBUILD** and **SC_BUILD_SCHEMAS**
-   **SC_SDAI_ADDITIONAL_EXES_SRCS** can be used to have SC build single-file executables (similar to p21read)
    -   this will not work for applications with more than one source code file or that need to link other libs.

#### See also: [CMake variables used by STEPcode](/docs/cmake_vars/)

## C++ examples

-   [Minimal Part 21 C++ example](Minimal_Part_21_C++_example.html)
-   doxygen documentation of [apps using STEPcode](http://stepcode.org/stepcode-use-doxygen/)
-   [sc/src/express/test](https://github.com/stepcode/stepcode/tree/master/src/express/test/)
    - tests for the express parser
-   [sc/test/cpp/](http://github.com/stepcode/stepcode/tree/master/test/cpp/)
    - tests written in c++; these can be built when ENABLE_TESTING is set to ON, but are excluded from 'make all'
-   [sc/src/test](http://github.com/stepcode/stepcode/tree/master/src/test)
    - tests written by NIST; all are up-to-date, but [p21read](https://github.com/stepcode/stepcode/blob/master/src/test/p21read/p21read.cc#L138) is the most frequently used. See the README in sc/src/test for more.
-   TODO: Example using lazy loading code. For now, see [lazy_test.cc](http://github.com/stepcode/stepcode/blob/master/src/cllazyfile/lazy_test.cc) in the repo.

## C++ applications that are not in the GitHub repository

The BRL-CAD [step-g](http://brlcad.svn.sourceforge.net/viewvc/brlcad/brlcad/trunk/src/conv/step/) converter, documented [here](http://stepcode.org/stepcode-use-doxygen/step-g_8cpp.html) (Note - currently, the BRL-CAD version of STEPcode differs slightly from the version on GitHub)

Laurent Bauer's [SCView](https://github.com/LaurentBauer/SCView/wiki)

## Python

-   [Python Generator](http://github.com/stepcode/stepcode/wiki/python-generator)

## TODO

-   describe use of [lazy loading code](http://github.com/stepcode/stepcode/blob/master/src/cllazyfile/lazyInstMgr.h)
-   create a page with a small Part 21 file, with description of format and links to relevant classes - SDAI_Application_instance, STEPcomplex, generated code (?)
-   run doxygen on parts of STEPcode (libexpress + exppp + fedex_plus, fedex_python, cllazyfile, cleditor, clstepcore + cldai + clutils + base ) **and automate doxygen with a script**

## See also

-   [Building STEPcode](/docs/building/)
-   [Testing](/docs/testing)
