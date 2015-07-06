---
title: Building STEPcode
layout: docs
permalink: /docs/building/
---

### Contents
* TOC
{:toc}


## Required packages

-   cmake \>= v2.8.7

-   As of v0.7, the following are no longer used:
    -   bison
    -   flex

## How to build

`cd sc
mkdir build
cd build
cmake ..    # '..' is the path to the directory containing the top-level CMakeLists.txt
make`

## Configuration options (append to the 'cmake ..' line):

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

## Create c++ for a schema manually:

`mkdir build/schema_name
cd build/schema_name
../bin/exp2cxx path/to/schema.exp`

## More details

For a walkthrough of the build process, see [Build Process](/docs/build_process/)

For a description of the contents of the build/ dir, see [Build Dir](/docs/build_dir/)

More options are available - see [Executables](/docs/executables/), and read comments in the various CMakeLists.txt files.
