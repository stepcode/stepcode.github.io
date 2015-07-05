---
title: Building STEPcode
layout: docs
permalink: /docs/building/
---

Required packages
-----------------

-   cmake \>= v2.8.7

-   As of v0.7, the following are no longer used:
    -   bison
    -   flex

How to build
------------

`cd sc
mkdir build
cd build
cmake ..    # '..' is the path to the directory containing the top-level CMakeLists.txt
make`

Configuration options (append to the 'cmake ..' line):
------------------------------------------------------

-   -DSC_BUILD_SCHEMAS="*path/to/schema.exp*;*path/to/schema2.exp*"
    -   For each schema listed, this
        -   generates c++
        -   compiles it into a library
        -   builds a 'p21read' program (see below)

    -   Will also work with directories, as long as each directory has a
        single express file. Multiple files/directories are separated by
        semicolons.

-   -DSC_BUILD_TYPE=[Debug\|Release\|RelWithDebInfo\|MinSizeRel]
    -   default is a Debug build
    -   Release turns on optimizations and strips out debugging
        information
    -   see also: cmake documentation for CMAKE_BUILD_TYPE

-   The above options can be used from the CMake GUI as well - just look
    through the list of variables.

#### See Also: [CMake variables](/docs/cmake_vars/)

Create c++ for a schema manually:
---------------------------------

`mkdir build/schema_name
cd build/schema_name
../bin/exp2cxx path/to/schema.exp`

Files created in build dir
--------------------------

-   `build/schema_scanner` a tool that writes CMakeLists.txt for each schema specified in SC_BUILD_SCHEMAS
    - this became necessary once exp2cxx was modified to produce individual files for each type/entity in the schema, as CMake can't handle compile-time determination of file names
    - you shouldn't ever have to run this by hand
-   `build/CMakeFiles` temporary files (i.e. `.o` files)
-   `build/src` same as build/CMakeFiles
-   `build/schemas/SCHEMA_NAME` generated source is written to files here
-   `build/bin/` executables
    - `exp2cxx` generates C++ code. Formerly *fedex_plus*
    - `exp2py` generates Python code. Formerly *fedex_python*
    - `exppp` Express Pretty Printer
        -   Normally, this isn't built
    - `check_express` Parses the express and checks for errors. Formerly *fedex*
        -   The functionality of exp2cxx/exp2py is a superset of this.
    - `p21read_sdai_SCHEMA_NAME` reads one step file and writes the contents to another
        - It may change whitespace or remove comments; otherwise, the input and output files are supposed to be identical. If they are not identical, either the file does not match the schema, or there is a bug in SC.
    - `lazy_sdai_SCHEMA_NAME` lazy loading test executable for SCHEMA
        - Prints time and memory statistics for various stages including file scanning. Loads a few instances, then exits.
-   `build/lib/` contains libraries, including libs created for schemas (prefixed with sdai)

More options are available - see the man pages, and read comments in the
various CMakeLists.txt files.
