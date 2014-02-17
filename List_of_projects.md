---
title: List of projects
---

|---|
|\_\_TOC\_\_|

STEPcode is participating in GSoC again!
========================================

Submit your GSoC 2014 proposal to the BRL-CAD organization but make it
clear that your proposal is for a STEPcode project.

For more information, see BRL-CAD's [GSoC
page](http://brlcad.org/wiki/Google_Summer_of_Code)

Project: code documentation
---------------------------

-   Brief Explanation: improve code documentation, utilize additional
    doxygen features

-   Expected Results: a 'make doxygen' target in CMake which will
    generate documentation (in HTML form, at least). This documentation
    will be greatly improved over the current documentation. It will be
    better organized and utilize many more of the features of doxygen -
    such as creating pages pertaining to specific topics. One example of
    the latter would be a page explaining our CMake-based build system.

-   Knowledge Prerequisite: Familiarity with doxygen, cmake, C, C++ a
    plus.

Project: exp2html
-----------------

-   Brief Explanation: documentation generator for EXPRESS

-   Expected Results: generate graphs and hyperlinked documentation of
    an express schema, including express comments (requires modifying
    parser to not skip comments). Outputs html + JavaScript (search,
    other?)

-   Knowledge Prerequisite: html, javascript, lexer and parser.

Project: minimal examples
-------------------------

-   Brief Explanation: create minimal examples for various schemas -
    such as AP214 or AP242 - in the style of
    [ap203min](http://github.com/stepcode/stepcode/blob/master/example/ap203min/ap203min.cpp)

-   Expected Results: an executable that writes a part 21 file that is
    compatible with the schema in question

-   Knowledge Prerequisite: EXPRESS, STEP, C++.

Project: ap242 support in BRL-CAD
---------------------------------

-   Brief Explanation: add support for AP242 to BRL-CAD's importer and
    exporter.

-   Expected Results: paragraph.

-   Knowledge Prerequisite: STEP, NURBS, C++

Project: refactor code
----------------------

-   Brief Explanation: split large files and functions, add unit tests,
    move contents of most or all LISTdo loops into separate functions.

-   Expected Results: smaller files and functions, greatly increased
    code coverage, more understandable code, less repeated code.

-   Knowledge Prerequisite: C, C++. Knowledge of code coverage tools
    such as lcov a plus.

Project: thread safety and performance
--------------------------------------

-   Brief Explanation: modify the libraries to improve thread safety,
    increase performance using hotspot analysis

-   Expected Results: possible to read/write files in different threads
    simultaneously; performance increase in single-threaded code

-   Knowledge Prerequisite: thread safety, C++. Valgrind or OProfile a
    plus.

Ideas for previous years
========================

If you are particularly interested in doing one of these now, contact us
- it might still be relevant.

Project: STEP CAD file viewer
-----------------------------

-   Brief Explanation: Develop a STEP CAD file viewer based on SCL for
    the latest STEP schemas 203ed2, 214ed3, and 242. Like IFCGears
    Viewer, it could use Qt and OpenSceneGraph for a desktop
    application. Or it could use WebGL in HTML5 for a browser front end
    like was demonstrated with pythonOCC. Using BRL-CAD as a modeling
    kernel is also an option.

-   Expected Results: A viewer that works with the latest STEP schemas
    and files.

-   Knowledge Prerequisite: SC currently supports C++ and python code
    generation.

Project: STEP-COLLADA direct bi-directional translation
-------------------------------------------------------

-   Brief Explanation: Translate directly between the leading neutral
    formats for mechanical CAD (STEP) and digital content creation
    (Collada)

-   Expected Results: Use SC and Collada open source code to develop a
    translator between STEP and COLLADA. Round-trip test with validated
    files from both formats.

-   Knowledge Prerequisite: SC currently supports C++ and python code
    generation.

Project: Data Probe Application
-------------------------------

-   Brief Explanation: A data instance graphical editor and EXPRESS
    schema browser

-   Expected Results: An application called Data Probe in SCL was an
    Instance Editor, but relied on an obsolete UI toolkit, InterViews.
    InterViews should be replaced by a modern toolkit like Qt, an IDE
    framework like Eclipse, or a web accessible front end. Support for
    both graphical editing of EXPRESS-G diagrams and text editing of
    their attributes is desired, along with contextual help derived from
    the EXPRESS schema.

-   Knowledge Prerequisite: SC supports C++, and python code generation.
    Some experience with Qt (or similar), Eclipse (or similar), or HTML5
    could be helpful.

Project: Part 21 (Exchange File) Test Coverage Generation and Reporting
-----------------------------------------------------------------------

-   Brief Explanation: Generate an instance file library for test
    coverage of an EXPRESS schema

-   Expected Results: Testing translators and other implementations
    based on SC requires a library of test cases. Given an EXPRESS
    schema, generate part21 files and validate them against the schema
    and analyze the test coverage of the part21reader. Use random and/or
    structured generation methods to enhance test coverage.

-   Knowledge Prerequisite: SC currently supports C++ and python code
    generation.

Project: Part 11 (EXPRESS) Test Coverage Generation and Reporting
-----------------------------------------------------------------

-   Brief Explanation: Generate an EXPRESS schema library for test
    coverage of the parser

-   Expected Results: Generate schemas to test the parser in
    \`libexpress\`. Possibly use the techniques discussed in J. Riehl's
    thesis [Grammar Based Unit Testing for
    Parsers](http://people.cs.uchicago.edu/~jriehl/thesis.pdf). Validate
    the schemas against the EBNF using
    [bnfparser2](http://bnfparser2.sourceforge.net/). Analyze test
    coverage of \`libexpress\` and \`exp2cxx\`. Validate the code
    generated by exp2cxx.

-   Knowledge Prerequisite: Familiarity with lemon parser (not terribly
    different from the bison parser), C, C++.

Project: Generate Part28 XML schema and documents
-------------------------------------------------

-   Brief Explanation: Generate a part28 XML schema from an EXPRESS
    schema and generate a part28read program

-   Expected Results: Like how SC already generates C++ and python
    libraries and a p21read program, extend the capability to the
    alternate part28 XML schema standard and a p28read program. Develop
    an application that converts between p21 and p28.

-   Knowledge Prerequisite: SC currently supports C++ and python code
    generation.

Project: Database Persistence
-----------------------------

-   Brief Explanation:

-   Expected Results: Implement database persistence of SC instance
    data. Use existing SDAI standard by extending SC, or experiment with
    SQLite, NoSQL or other methods. Develop a demonstration application
    that reads part21 instance data files and persists and manages them
    in a database.

-   Knowledge Prerequisite: SC currently supports C++ and python code
    generation. Database implementation experience would be helpful.

Project: Multithread/Multiprocess Part21 import/export.
-------------------------------------------------------

-   Brief Explanation: Part21 huge files (hundreds of Mb) are known to
    be heavily resource consuming (in terms of computing time or memory
    consumption) when being imported. The memory consumption issue can
    be solved by some kind of database persistence (see above the
    "Database Persistence" project). This project aims at reducing the
    computing time by using multithread and multiprocess programming
    techniques. Student will have to complete the current python
    implementation in order to support this performance improvement.
    Student will have a look at the threading and multiprocessing python
    modules (part of the python Standard Library) as well as pycluster
    (http://bonsai.hgc.jp/\~mdehoon/software/cluster/software.htm).

-   Expected Results: student should achieve an (almost) linear
    reduction of computing time according to the number of
    threads/cores. The project will be considered as successful if the
    demonstration application achieves at least 50% reduction on a 2
    cores machine (whatever the number of threads/processes may be).

-   Knowledge Prerequisite: python experience. Multithreading
    programming.

Project: Quality Assurance for STEP files/SCL library
-----------------------------------------------------

-   Brief Explanation: STEP is the most famous data model used in the
    whole industry to exchange product data (MCAD or ECAD data, finite
    element experiments etc.). We all, STEP users, use to deal with
    "wrong" STEP files: the Part21 file generated from the software 1
    cannot be imported into the software 2, and we're not even able to
    explain whether the issue come from the software 1, or the software
    2, or both! Ensuring the quality of a STEP Part21 file is then a
    requirement if the purpose is to keep the control of engineering
    data over their whole lifecycle. What do we mean with 'quality' of a
    STEP Part21 file? It \*must absolutely\* comply with the EXPRESS
    schema semantics. Attributes type checking is only a part of the
    job: where/rules, unique and inverse attributes also have to be
    checked. Student will have to complete python generator to support
    these features, and will take care to heavily unit-test the new
    developments.

-   Expected Results: student will develop a program which takes a
    Part21 file and the related express schema. This program will output
    an analysis report about STEP file quality.

-   Knowledge Prerequisite: python and C++ programing. Test driven
    development.

* * * * *

* * * * *

Project: TEMPLATE
-----------------

-   Brief Explanation: paragraph.

-   Expected Results: paragraph.

-   Knowledge Prerequisite: paragraph.

