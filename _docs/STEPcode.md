---
layout: docs
title: Welcome
permalink: /docs/home/
---

----

The **STEPcode** project is a collection of open source libraries, tools, and resources that revolve around the technologies of [ISO 10303](http://en.wikipedia.org/w/index.php?title=ISO_10303), a.k.a. STEP, the **ST**andard for the **E**xchange of **P**roduct model data.

STEPcode provides a cross-platform (Linux, OSX, **and** Windows) implementation of

-   an EXPRESS schema parser with bindings provided in C, C++, and
    Python
-   libraries containing classes to represent SDAI (Part 22) objects
-   a library that allows STEP Part 21 files to be read and written
-   various utilities, test routines, and test schemas


The [BSD license](http://github.com/stepcode/stepcode/blob/master/COPYING) allows commercial use. In addition, STEPcode is used in other open source projects such as [BRL-CAD](http://www.brl-cad.org) and [SCView](http://github.com/LaurentBauer/SCView).  

STEPcode traces its roots to the NIST STEP Class Library (SCL) which was developed between ~1987 and 1998.

See also: [History](History.html), [List of external resources](List_of_external_resources.html), [List of OSS or free STEP programs](List_of_OSS_or_free_STEP_programs.html)

### Quick Start

-   See the [basic usage](/docs/usage/) page


STEP & Other Standards
----------------------

STEP can be used for neutral file exchange or as a basis for data sharing or archiving in areas such as drafting, mechanical and assembly design, electromechanical design, machine tool control, PLCS (product lifecycle support), systems engineering, computational fluid dynamics and finite element analysis. Parts of the STEP specification are reused in other standards, so STEPcode use is not limited to ISO 10303.

STEPcode can be used with the following standards because they reuse [Part 11](http://en.wikipedia.org/wiki/ISO_10303-11) and [Part 21](http://en.wikipedia.org/wiki/ISO_10303-21) of ISO 10303:

-   AP203, AP214 and AP242 for CAD tested at the
    [CAX-IF](http://www.cax-if.org)
-   [AP210](http://www.wikistep.org/index.php/Main_Page#AP210_specifics)
-   The Industry Foundation Classes (**IFC**),used for Building Information Modeling (**BIM**)
-   ISO 15926, used in the Oil & Gas industry
-   STEP-TAS, used in the thermal analysis of aerospace equipment
-   ISO 13584, *Industrial automation systems and integration - Parts library*
-   [ISO 13399](http://en.wikipedia.org/wiki/ISO_13399)

Some schemas are [included](/docs/included_schemas/) with STEPcode, but those are not the only ones that it will work with.

# Community
---------

The [scl-dev mailing list](http://groups.google.com/forum/?fromgroups#!forum/scl-dev) is hosted on google groups. In spite of the name, this is for both users and developers. The STEPcode project has evolved into a diverse open source community helping improve the accessibility, adoption, and long-term availability of STEP related technologies for CAx developers.

#### [Projects](List_of_projects.html) and [tasks](List_of_tasks.html)

# Code
--------

**The source code is on [GitHub](http://github.com/stepcode/stepcode)**

More pages:
----

-   [Getting started](Getting_started.html)
-   [Building STEPcode](Building_STEPcode.html)
-   [Description of the files and directories](Files_and_directories.html)
-   [How to use STEPcode in an application](How_to_use_STEPcode_in_an_application.html)

We use [Travis-CI](https://travis-ci.org/stepcode/stepcode) for testing. It automatically tests pull requests, and tests master when it changes. Originally, we used a [CDash dashboard](http://my.cdash.org/index.php?project=StepClassLibrary) to show the status of test runs. Test results are only visible for a month, and it was difficult to navigate.

Links
-----

-   [WikiSTEP](http://wikistep.org/) - wiki for the STEP standard
-   [STEP on Wikipedia](http://en.wikipedia.org/w/index.php?title=ISO_10303)


# FIXME organize these

[Other free STEP-related software](/docs/other_free_step/)

[Minimal Part 21 C++ example](/docs/p21_cpp_example/)

[P21Read](/docs/p21read/)
