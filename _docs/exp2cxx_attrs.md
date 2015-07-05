---
layout: docs
permalink: /docs/code/exp2cxx_attrs/
title: Attributes in exp2cxx
---

This comes from
[classes_misc.c:709](https://github.com/stepcode/stepcode/blob/master/src/fedex_plus/classes_misc.c#L709).
It should be formatted such that doxygen sees it.

Attributes are divided into four categories: these are not exclusive as
far as I can tell! I added defs below DAS

-   simple explicit
-   type shifters
    -   not DERIVEd - redefines type in ancestor
    -   VARget_initializer(v) returns null

-   simple derived
    -   DERIVEd - is calculated - VARget_initializer(v)
    -   returns non-zero, VARis_derived(v) is non-zero

-   overriding
    -   includes type shifters and derived

All of them are added to the dictionary. Only type shifters generate a
new STEPattribute. Type shifters generate access functions and data
members, for now. Overriding generate access functions and data members,
for now. *???? DAS*

### type shifting attributes

Before printing new STEPattribute, check to see if it's already printed
in supertype.

Still add new access function.

### overriding attributes

Go through derived attributes. If STEPattribute found with same name,
tell it to be * for reading and writing
