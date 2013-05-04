---
title: How to test with CTest
---

Without ctest script
--------------------

**Preferred method**

-   configure with SC\_ENABLE\_TESTING=ON, i.e.

`cmake .. -DSC_ENABLE_TESTING=ON`

-   build:

`make`

-   run tests:

`make test`

-   results will look like

`  Running tests...
  Test project /opt/step/test-sc/build_ctest
          Start   1: generate_cpp_ap239_arm_lf
    1/137 Test   #1: generate_cpp_ap239_arm_lf ........................................   Passed    3.55 sec
          Start   2: build_cpp_sdai_ap239_arm_lf
    2/137 Test   #2: build_cpp_sdai_ap239_arm_lf ......................................   Passed   84.97 sec`
... `  Label Time Summary:
  cpp_schema_build       = 932.95 sec
  cpp_schema_gen         =  37.66 sec
  cpp_schema_rw          =  42.59 sec
  cpp_schema_specific    =  10.50 sec
  exchange_file          =   0.49 sec
  unitary_schemas        =   0.24 sec
  
  Total Test time (real) = 1025.09 sec
  
  The following tests FAILED:
            7 - read_write_cpp_ap227_mitre (Failed)
           33 - read_write_cpp_ap210e2_v1_40_mim_lf_SurfaceMountFlasher (Failed)
           34 - read_write_cpp_ap210e2_v1_40_mim_lf_PDES-181 (Failed)`
and so on.

Via ctest script
----------------

**Note:** this is not recommended, as results are not reported unless
result submission is enabled and you look at
[my.cdash.org](http://my.cdash.org/index.php?project=StepClassLibrary)
after running the tests. From the **STEPcode/** dir, run CTest:
`ctest -S run_ctest.cmake`

It will warn you that .SC\_CTEST\_PREFS.cmake is missing. This is
normal, unless you are set up to submit test results to my.cdash.org.
Free my.cdash.org accounts have limits on the number of people that are
allowed to submit tests, so please discuss on the mailing list before
you create the file.
