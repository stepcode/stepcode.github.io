---
title: STEPcode CMake variables
---

You can change these
--------------------

### SC\_BUILD\_SCHEMAS

-   List of schemas to be built. Defaults to special value ALL, which
    builds all schemas in SC/data.
-   Each list entry can be a relative or absolute path to a schema or to
    a directory. If an entry is a directory, CMake looks for **\*.exp**
    within that directory.

### SC\_BUILD\_TYPE

-   Release, Debug, etc.
-   See also: CMAKE\_BUILD\_TYPE documentation

### SC\_GENERATE\_LEXER\_PARSER

-   See comments in root CMakeLists.txt for this variable.

### SC\_INSTALL\_PREFIX

-   prefix for 'make install'

### SC\_IS\_SUBBUILD

-   used when building as a subproject, as SCView and BRL-CAD do.
-   example of use:
    <http://github.com/LaurentBauer/SCView/blob/master/CMakeLists.txt>

### SC\_MEMMGR\_ENABLE\_CHECKS

-   enables runtime memory leak checks. Output is very verbose!

### SC\_SDAI\_ADDITIONAL\_EXES\_SRCS

-   list of paths to source files for additional executables that will
    be built for each schema. Each source file is assumed to be
    stand-alone, much like p21read.cc

Variables exclusively for CTest
-------------------------------

These won't do anything useful unless you're running tests.

### SC\_ENABLE\_COVERAGE

-   for code coverage tests; requires gcov/lcov -
    <http://ltp.sourceforge.net/coverage/lcov.php>

`ctest -S lcov.cmake`

### SC\_ENABLE\_TESTING

-   tests can be run manually (no submission) by setting this to ON,
    then

`make
make test`

-   also set by CTest - see [How to test with
    CTest](How to test with CTest "wikilink")

You probably don't want to change these
---------------------------------------

### SC\_ABI\_SOVERSION

### SC\_BASE\_SOURCES

### SC\_BINARY\_DIR

### SC\_CMAKE\_DIR

### SC\_SOURCE\_DIR

### SC\_VERSION\_MAJOR

### SC\_VERSION\_MINOR
