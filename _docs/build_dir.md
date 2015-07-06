---
title: Build Dir contents
layout: docs
permalink: /docs/build_dir/
---

### Contents
* TOC
{:toc}

The build directory is the directory that cmake is executed from, if executed from the command line.

## schema_scanner
- a tool that writes CMakeLists.txt for each schema specified in SC_BUILD_SCHEMAS
    - this became necessary once exp2cxx was modified to produce individual files for each type/entity in the schema, as CMake can't handle compile-time determination of file names
    - you shouldn't ever have to run this by hand

## CMakeFiles
- temporary files (i.e. `.o` files)

## src
- same as CMakeFiles

## schemas/SCHEMA_NAME
- generated source is written to files here

## bin/
See [executables](/docs/executables/)
<!--    - `exp2cxx` generates C++ code. Formerly *fedex_plus*
    - `exp2py` generates Python code. Formerly *fedex_python*
    - `exppp` Express Pretty Printer
        -   Normally, this isn't built
    - `check_express` Parses the express and checks for errors. Formerly *fedex*
        -   The functionality of exp2cxx/exp2py is a superset of this.
    - `p21read_sdai_SCHEMA_NAME` reads one step file and writes the contents to another
        - It may change whitespace or remove comments; otherwise, the input and output files are supposed to be identical. If they are not identical, either the file does not match the schema, or there is a bug in SC.
    - `lazy_sdai_SCHEMA_NAME` lazy loading test executable for SCHEMA
        - Prints time and memory statistics for various stages including file scanning. Loads a few instances, then exits.-->

## lib/
- contains libraries, including libs created for schemas (prefixed with sdai)
