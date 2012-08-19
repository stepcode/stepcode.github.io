---
title: How to test with CTest
---

From the **STEPcode/** dir, run CTest:

**ctest -S run\_ctest.cmake**

It will warn you that .SCL\_CTEST\_PREFS.cmake is missing. This is
normal, unless you intend to submit test results to my.cdash.org. Note -
free my.cdash.org accounts have limits on the number of people that are
allowed to submit tests.
