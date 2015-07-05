---
title: Attributes in fedex plus
---

This comes from
[classes\_misc.c:709](https://github.com/stepcode/stepcode/blob/master/src/fedex_plus/classes_misc.c#L709).
It should be formatted such that doxygen sees it.

Attributes are divided into four categories: these are not exclusive as
far as I can tell! I added defs below DAS

-   simple explicit
-   type shifters
    -   not DERIVEd - redefines type in ancestor
    -   VARget\_initializer(v) returns null

-   simple derived
    -   DERIVEd - is calculated - VARget\_initializer(v)
    -   returns non-zero, VARis\_derived(v) is non-zero

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
tell it to be \* for reading and writing

[Category:Code discussion](Category:Code_discussion.html)
