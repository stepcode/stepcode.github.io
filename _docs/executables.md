---
title: Executables
layout: docs
permalink: /docs/executables/
---

### Contents
* TOC
{:toc}

See also: [Build Dir](/docs/build_dir/)

These executables reside within `build/bin/`.

## exp2cxx
- generates C++ code. Formerly *fedex_plus*
- See also - [libexpress common options](#libexpress-common-options)

`usage: exp2cxx common_options [-s|-S] [-a|-A] [-c|-C] [-L] express_file
where   -s or -S uses only single inheritance in the generated C++ classes
        -a or -A generates the early bound access functions for entity classes the old way (without an underscore)
        -c or -C generates C++ classes for use with CORBA (Orbix)
        -L prints logging code in the generated C++ classes
`

## exp2python
- generates Python code. Formerly *fedex_python*
- See also - [libexpress common options](#libexpress-common-options)

`usage: exp2python common_options express_file`

## exppp
- Express Pretty Printer
- See also - [libexpress common options](#libexpress-common-options)

`usage: exppp common_options [-l _length_] [-c] [-o [file|--]] express_file
        -l specifies line length hint for output
        -t enable tail comment for declarations - i.e. END_TYPE; -- axis2_placement
        -c for constants, print one item per line (YMMV!)
        -o specifies the name of the output file (-- for stdout)
`

## check_express
- Parses the express and checks for errors. Formerly *fedex*
-   The functionality of exp2cxx/exp2python is a superset of this.
- See also - [libexpress common options](#libexpress-common-options)

`usage: check-express common_options express_file`

## p21read_sdai_SCHEMA_NAME
- reads one step file and writes the contents to another
- It may change whitespace or remove comments; otherwise, the input and output files are supposed to be identical. If they are not identical, either the file does not match the schema, or there is a bug in SC.
- TODO document args

## lazy_sdai_SCHEMA_NAME
- lazy loading test executable for SCHEMA
- Prints time and memory statistics for various stages including file scanning. Loads a few instances, then exits.
- TODO document args

## libexpress common options
Executables linked with libexpress share some common options, though they don't all make sense for every executable.

`usage: _executable_ [-v] [-d #] [-n] [-p _object_type_] [-w|-i _warning_]`

`-v produces a version description
-d turns on debugging ("-d 0" describes this further
-n do not pause for internal errors (useful with delta script)
-p turns on printing when processing certain objects (see below)
-w warning enable
-i warning ignore`

_warning_ is one of

`none
all
circular_subtype
circular_select
entity_as_type
invariant_condition
invalid_case
unnecessary_qualifiers
downcast
indexing
unsupported
limits`

_object_type_ is one or more of

`e       entity
p       procedure
r       rule
f       function
t       type
s       schema or file
#       pass #
E       everything (all of the above)`

Version description will be similar to
`Build info for build/bin/exp2cxx: git commit id: v0.8-116-g35170b3, build timestamp 05 Jul 2015 22:14
http://github.com/stepcode/stepcode and scl-dev on google groups
`