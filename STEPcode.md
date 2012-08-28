---
title: STEPcode
---

|---|
|\_\_TOC\_\_|

Introduction
------------

The **STEPcode** project is a collection of open source libraries,
tools, and resources that revolve around the technologies of [ISO
10303](http://en.wikipedia.org/w/index.php?title=ISO_10303), a.k.a.
STEP. Parts of the STEP specification are reused in other standards, so
STEPcode use is not limited to ISO 10303.

STEPcode provides a robust implementation of

-   an EXPRESS schema parser with bindings provided in C, C++, and
    Python
-   additional libraries that allow STEP Part 21 files to be read and
    written
-   various utilities, test routines, and test schemas

The [BSD
license](http://github.com/stepcode/stepcode/blob/master/COPYING) allows
commercial use. In addition, STEPcode is used in other open source
projects such as [BRL-CAD](http://www.brl-cad.org).

### STEP & Other Standards

ISO 10303 is commonly referred to as **STEP**, the **ST**andard for the
**E**xchange of **P**roduct model data. It can be used for neutral file
exchange or as a basis for a data sharing or archiving in areas such as
drafting, mechanical and assembly design, electromechanical design,
machine tool control, PLCS (product lifecycle support), systems
engineering, computational fluid dynamics and finite element analysis.

STEPcode can be used with the following standards because they reuse
[Part 11](http://en.wikipedia.org/wiki/ISO_10303-11) and [Part
21](http://en.wikipedia.org/wiki/ISO_10303-21) of ISO 10303:

-   AP203, AP214 and AP242 for CAD [1](http://www.cax-if.org)
-   The Industry Foundation Classes (**IFC**) are used for Building
    Information Modeling (BIM)
-   ISO 15926 is used in the Oil & Gas industry
-   STEP-TAS is used in the thermal analysis of aerospace equipment
-   ISO 13584, *Industrial automation systems and integration - Parts
    library*
-   [ISO 13399](http://en.wikipedia.org/wiki/ISO_13399)

### Community

Based originally on the NIST STEP Class Library (SCL), the STEPcode
project has evolved into a diverse open source community helping improve
the accessibility, adoption, and long-term availability of STEP related
technologies for CAx developers.

See also: [History](History "wikilink")

### Using STEPcode

-   [How to use STEPcode in an
    application](How to use STEPcode in an application "wikilink")

### Documentation

-   **[Doxygen](http://stepcode.org/doxygen/)** for v0.6
-   doxygen documentation of [apps using
    STEPcode](http://stepcode.org/stepcode-use-doxygen/)
-   See also [:Category:Code
    discussion](:Category:Code discussion "wikilink")

### Schemas

There is a [list of schemas](list of schemas "wikilink") that STEPcode
has been tested with.

### To Do

There is a **[list of tasks](list of tasks "wikilink")** that involve
improving the wiki or STEPcode's source code. In addition, there is a
**[list of projects](list of projects "wikilink")** that are more
difficult than the tasks; these might be appropriate for GSoC
participants.

Links
-----

-   The source code is on [GitHub](http://github.com/stepcode/stepcode)
    -   Any discussion of the code on this wiki should have a
        [[Category:Code discussion]] tag so that it shows up in
        [:Category:Code
        discussion](:Category:Code discussion "wikilink")

-   The [<http://groups.google.com/forum/?fromgroups>\#!forum/scl-dev
    mailing list] is hosted on google groups.
-   We have a [CDash
    dashboard](http://my.cdash.org/index.php?project=StepClassLibrary)
    do show the status of recent test runs.
    -   Unfortunately, it is not possible to view tests from more than
        one day at once; you must use the **Previous** link for that.
        Testing is sporadic, and is generally only done for branches
        that are under review.

External Resources
------------------

A [list of external resources](list of external resources "wikilink")
related to STEP/EXPRESS.
