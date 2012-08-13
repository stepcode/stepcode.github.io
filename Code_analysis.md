---
title: Code analysis
---

Tools that analyze hotspots, memory issues, code coverage, etc

Cross Platform
==============

ctest/cdash (testing)
---------------------

-   install cmake/ctest, then run 'ctest -S run\_ctest.cmake'
-   test submission to my.ctest.org requires creation of a file in the
    dir above the STEPcode source; read the messages from the above
    command

Linux-only
==========

callgrind (find hotspots)
-------------------------

For best results, install kcachegrind for visualization. Requires KDE.
`valgrind --tool=callgrind bin/p21read_sdai_AP214E3_2010 ../data/ap214e3/as1-oc-214.stp 
kcachegrind callgrind.out.<pid>     #don't use a wildcard if more than one callgrind file exists!`

massif (find where the most memory is allocated)
------------------------------------------------

Install valgrind, kgraphviewer, massif-visualizer. Install valgrind from
your distro. The other two are probably not available in your distro; in
addition, they require Qt, KDE, and graphviz-dev.

-   build kgraphviewer:

`git clone http://anongit.kde.org/kgraphviewer
cd kgraphviewer
mkdir build
cd build
cmake ..
make
sudo make install  #this defaults to installing under /usr/local`

-   build massif-visualizer:

`git clone http://anongit.kde.org/massif-visualizer
cd massif-visualizer
mkdir build
cd build
cmake ..  #after this step, verify that kgraphviewer was found
make
sudo make install  #this defaults to installing under /usr/local`

-   run massif and visualize:

`valgrind --tool=massif bin/p21read_sdai_AP214E3_2010 ../data/ap214e3/as1-oc-214.stp
massif-visualizer massif.out.<pid>`

lcov/gcov (code coverage)
-------------------------

`ctest -S lcov.cmake
# 30 minutes later, open the resulting html file in a browser`

Downloads
=========

Output of callgrind, cachegrind, and massif:
<https://docs.google.com/open?id=0B9G1tTILtiCyTmhoLTZva0JxdTQ>

[Category:Code discussion](Category:Code discussion "wikilink")
