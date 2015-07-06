---
title: Build Process
layout: docs
permalink: /docs/build_process/
---

### Contents
* TOC
{:toc}

## A bit of history

When NIST wrote the STEP Class Libraries, libexpress, fedex_plus, etc, they used makefiles and shell scripts to control the build process. While this allowed them to easily automate the build process, it was not portable.

STEPcode, the renamed STEP Class Libraries, now use CMake. CMake is portable, but does impose some restrictions that were not originally present.

fedex_plus (now exp2cxx) originally wrote a Makefile fragment containing the names of the generated files. Make would happily use that fragment while compiling the Libraries. At that time, a few large files were generated - but the Makefile fragment meant it would have been relatively easy to split the code into numerous small files. Because CMake must create native build system files before the code generation process begins, it is not possible to utilize the Makefile fragment trick. We included some code in CMake to guess what the file names would be, and it ended up working well. However, splitting up the generated code was a priority and it was not feasible to extend this CMake code to that task.

To work around this, we wrote a parser which is built and executed during the configure stage - before CMake has finished reading its files - that reads each EXPRESS input file (schema), determines file names for each TYPE, ENTITY, etc, and writes a CMakeLists.txt. After the CMakeLists.txt is written, add_subdirectory() is called for the dir containing it. CMake is unaware that the file didn't exist until the external command executed; it loads the generated CMakeLists.txt as it would any other file.

## The process

When CMake runs, all files are written to the [build dir](/docs/build_dir/). First, CMake checks for headers and libraries just like any normal configure process. After that, it checks SC_BUILD_SCHEMAS. If that variable is empty, it defaults to generating and compiling code for every schema it can find. Otherwise, it treats the variable as a semicolon-separated list of schemas to be processed. For each schema, it runs the schema scanner (above), generating a CMakeLists.txt.

Depending on options, various libs and tools may or may not be selected for compilation. CMakeLists.txt are processed and native build system files are created. When the src/express CMakeLists.txt is processed, the lexer and parser input files, as well as the code in src/express/generated, are compared against stored hashes. If any of those hashes differ, it indicates that the lexer or parser was modified and the code must be re-generated. If that is true, CMake will stop with an error unless it found perplex, lemon, and re2c. If those were found, they are used to regenerate the code, and then the stored hashes are updated with new values.

If code for schemas is to be generated, exp2cxx (or exp2py) must be compiled first. Both of those depend on the lexer/parser in libexpress. Once code is generated, it can be compiled and linked into what is commonly referred to (in STEPcode) as an SDAI library. This name refers to the fact that the code conforms to the API dictated by Part 22, Standard Data Access Interface. SDAI libraries also link against `src/cl*`, the [class libraries](/docs/files_dirs/#class-libraries).
