---
layout: docs
title: Basic Usage
permalink: /docs/usage/
---

## Prerequisites

More details: [prerequisites](/docs/prereqs/).

* Install git (windows: msysgit or GitHub Bootcamp, detailed in prerequisites)
* Install CMake
* Clone the repo

## Build

More details: [building STEPcode](/docs/building/).

Create a build dir inside the STEPcode dir. From there, run `cmake ..` or `cmake-gui`. Schemas are selected with the variable `SC_BUILD_SCHEMAS`. Once CMake has finished without error, use your build system (make, MSVC, etc) to compile.

## Use

See [examples](/docs/examples/)

## Explore

More details: [description of the files and directories](/docs/files_dirs/)
