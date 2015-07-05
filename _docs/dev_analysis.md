---
layout: docs
permalink: /docs/code/dev_analysis/
title: Code analysis
---

Tools that analyze hotspots, memory issues, code coverage, etc

## Cross Platform

### CTest (run tests)

- Install CMake and CTest
- Enable testing when you run CMake (`SC_ENABLE_TESTING=ON`)
- Build the test target (i.e. `make test`)
- On GitHub, PR's are automatically tested with Travis-CI and Appveyor.

## Linux-only

### callgrind (find hotspots)

For best results, install kcachegrind for visualization. Requires KDE.
{% highlight bash %}
valgrind --tool=callgrind bin/p21read_sdai_AP214E3_2010 ../data/ap214e3/as1-oc-214.stp 
kcachegrind callgrind.out.<pid>     #don't use a wildcard if more than one callgrind file exists!
{% endhighlight %}

### massif (find where the most memory is allocated)

Install valgrind, kgraphviewer, massif-visualizer. Install valgrind from
your distro. The other two are probably not available in your distro; in
addition, they require Qt, KDE, and graphviz-dev.

-   build kgraphviewer:

{% highlight bash %}
git clone http://anongit.kde.org/kgraphviewer
cd kgraphviewer
mkdir build
cd build
cmake ..
make
sudo make install  #this defaults to installing under /usr/local
{% endhighlight %}

-   build massif-visualizer:

{% highlight bash %}
git clone http://anongit.kde.org/massif-visualizer
cd massif-visualizer
mkdir build
cd build
cmake ..  #after this step, verify that kgraphviewer was found
make
sudo make install  #this defaults to installing under /usr/local
{% endhighlight %}

-   run massif and visualize:

{% highlight bash %}
valgrind --tool=massif bin/p21read_sdai_AP214E3_2010 ../data/ap214e3/as1-oc-214.stp
massif-visualizer massif.out.<pid>
{% endhighlight %}

### lcov/gcov (code coverage)

{% highlight bash %}
ctest -S lcov.cmake
# 30 minutes later, open the resulting html file in a browser
{% endhighlight %}

## Downloads

Output of callgrind, cachegrind, and massif:
<https://docs.google.com/open?id=0B9G1tTILtiCyTmhoLTZva0JxdTQ>
